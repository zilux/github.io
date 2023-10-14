---
title: "Collections"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

![Process_Mem](/images/git.png)


# Installing collections

Install collections for "local use"  from galaxy/git or hub.


## from galaxy with collection on cmd-line

```
$ ansible-galaxy collection install community.crypto
$ ansible-galaxy collection install /tmp/community-dns-1.2.0.tar.gz -p ./collections
```

## From galaxy by requirements file

```
ansible-galaxy collection install -r requirements.yml -p ./collections

requirements.yml:
---
collections:
  - name: community.crypto
    version: 1.0.2
```



## from git by command-line:

```
$ ansible-galaxy collection install git@github.com:zilux/ziluxtool_collection.git -p ./collections
```


## from git by requirements.yml:

```
ansible-galaxy collection install -r requirements.yml -p ./collections

requirements.yml
---
collections:
  - name: git@github.com:zilux/ziluxtools_collection.git
    type: git
```


## from git by requirements.yml where "galaxy.yml" is located

```
---
collections:
  - name: git@github.com:zilux/justtest.git#/collections/ansible_collections/zilux/tools
    type: git
```


## Show local installed collecitons

```
$ ansible-galaxy collection list
```



When RUNNING playbook ansible looks in ./collections
then via  collections_paths  uit ansible.cfg

collections_paths = ./collections:/usr/share/ansible/collections

Will be in stalled in first part of ./collections_paths

If not set it defaults to  ~/.ansible/collections:/usr/share/ansible/collections



The default is to install with ansible-galaxy but you can specify this in ansible.cfg ( galaxy or hub )

```
[galaxy]
server_list = automation_hub, galaxy

[galaxy_server.automation_hub]
url=https://console.redhat.com/api/automation-hub/
auth_url=https://sso.redhat.com/auth/realms/redhat-external/protocol/openid-connect/token 3
token=eyJh...Jf0o 4

[galaxy_server.galaxy]
url=https://galaxy.ansible.com/
```



======================================================================================


# Create collection

```
ansible-galaxy collection init training.web

ansible-galaxy role init training/web/roles/pipo
```


Then edit training/web/galaxy.yml for dependencies:

```
...
dependencies:
  ansible.posix: '>=1.0.0'
```

If plugins/lookup/qrcode.py are needed:

Create requirements.txt for Python modules dependencies

```
requirments.txt
pillow
qrcode
```

Create meta/runtime.yml
```
requires_ansible: '>=2.9.10'
```


If e.g. rpm's are needed:
```
content bindep.txt:

rsync [platform:centos-8 platform:rhel-8]
of
rsync [platform:rpm]
```


Create collection:

```
ansible-galaxy collection build
```


You can upload this to hub/galaxy after creating namespace and approve it.

{{< button relref="/" >}}Go Home{{< /button >}}

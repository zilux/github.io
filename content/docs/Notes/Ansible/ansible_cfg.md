---
title: "ansible.cfg"
weight: 5 
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

#    ![Process_Mem](/images/git.png)


# {{< button relref="/" >}}Go Home{{< /button >}}


## Example ansible.cfg


```
[defaults]
inventory = hosts
roles_path = roles
collections_paths = ./collections:/usr/share/ansible/collections
retry_files_enabled = False
host_key_checking = False
ansible_managed = "Ansible managed using role"
remote_user = harry
display_skipped_hosts = yes
display_ok_hosts = yes

[ssh_connection]
pipelining = True

[galaxy]
server_list = ng

[galaxy_server.ng]
url = https://galaxy.ansible.com/api/
token= xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

#
# https://ansible.readthedocs.io/projects/galaxy-ng/en/latest/community/userguide/#api
#
# # Find all roles created by a specific github user.
# curl 'https://galaxy.ansible.com/api/v1/roles/?github_user=geerlingguy' | jq

# Find all roles containing a keyword in the namespace, name or description.
# curl 'https://galaxy.ansible.com/api/v1/roles/?keyword=docker' | jq
#
#
# ansible-galaxy role search --help
#
#
# ansible-galaxy collection publish --help
#
#
```

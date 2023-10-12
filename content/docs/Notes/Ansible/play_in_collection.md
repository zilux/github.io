---
title: "use playbook in collection"
weight: 2
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

![Process_Mem](/images/git.png)


# Playbook calling play in collection

Play source vars in in first play which are also seen in play2 (import_playbook)

```
---
- name: Run play in playbooks from collection qrom.test
  hosts: localhost
  tasks:
    - ansible.builtin.debug:
        msg: play1

    - include_vars: pipo.yml

- name: Import a playbook
  ansible.builtin.import_playbook: qrom.test.tester
```


## pipo.yml

This file contains:

```
geheim=xxxxx
```


## playbooks/tester.yml

The content of collections/ansible_collections/qrom/test/playbooks/tester.yml

```
---
- name: Tester in Playbooks
  hosts: localhost
  gather_facts: false
  collections:
    - qrom.tester
  vars_files:
    "{{ playbook_dir }}/pipo.yml"

  tasks:

    - name: Some debug
      debug:
        msg: We are doing ... {{ playbook_dir }} .

    - name: Import a role
      ansible.builtin.import_role:
        name: tester
      vars:
        melding: not to much

    - name: Some debug
      debug:
        msg:  geheim is {{ geheim|default("nvt") }}
```

### Output

The output looks like this:


```
output:
LAY [localhost] **********************************************************************************************************************************************************************************************************************

TASK [Gathering Facts] ****************************************************************************************************************************************************************************************************************
ok: [localhost]

TASK [ansible.builtin.debug] **********************************************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "play1"
}

TASK [include_vars] *******************************************************************************************************************************************************************************************************************
ok: [localhost]

PLAY [Tester in Playbooks] ************************************************************************************************************************************************************************************************************

TASK [Some debug] *********************************************************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "We are doing ... /data/ANSIBLE/tempie/collections/ansible_collections/qrom/test/playbooks ."
}

TASK [qrom.test.tester : Debug info] **************************************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "not to much"
}

TASK [Some debug] *********************************************************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "geheim is xxxxx"
}
```

---
title: "Using roles/collections"
weight: 10 
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---


## Using roles in playbooks

### with roles statement

```
---
- name: Use collection
  hosts: localhost

  roles:
    - hz.coll.pipo
    - mgrole
    - role: foo
      vars:
        dir: /opt/pipo
        app_port: 5001
      tags: mytag
```

Also like this ...

```
---
- name: Use roles
  hosts: localhost

  roles:
    - { role: foo, mes: 'aap' }
    - { role: nah, mes: 'noot' }
```     


### With include_role module

```
---
- name: include stuff
  include_role:
    name: foo_app
  vars:
    dir: /tmp/pipo
    port: 9090
  tags: 
    - tag1
    - tag2
```

### Include role and run task from it

```
- include_role:
    name: let_scammer
    task_from: invate.yml
```


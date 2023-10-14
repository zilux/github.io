---
title: "restic"
weight: 4
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

## restic

### Backup

```
mount /dev/sdb /mnt
restic -r /mnt/node1/restic-repo init
cd /home/pipo/ansible

restic -r /mnt/node1/restic-repo backup .

# dry-run
# restic -r /mnt/node1/restic-repo backup . -n -vv | grep added  ## dry-run


restic -r /mnt/node1/restic-repo/ backup /home/pipo/ansible --tag Ansible --tag node1
restic -r /mnt/node1/restic-repo/ backup /netgear/Bckup-Win --tag Bckup-Win --tag node1
restic -r /mnt/node1/restic-repo/ snapshots
```

### Show Backups

```
# restic -r /mnt/node1/restic-repo snapshots
enter password for repository:
repository d102ab89 opened successfully, password is correct
ID        Time                 Host           Tags        Paths
-----------------------------------------------------------------------------
e7be4fe6  2023-04-08 14:56:54  node1.pipo.nl              /home/pipo/ansible
-----------------------------------------------------------------------------
1 snapshots
 
```



## Restore

```
# restic -r /mnt/node1/restic-repo restore ca5afc62 --target /tmp/pipo/
```



## Browsing your backup

```
# mkdir /tmp/restic
# restic -r /mnt/node1/restic-repo mount /tmp/restic
```

## Removing Backups

```
$ restic -r /mnt/node1/restic-repo/ snapshots
ID        Time                 Host           Tags        Paths
-----------------------------------------------------------------------------
e7be4fe6  2023-04-08 14:56:54  node1.pipo.nl              /home/pipo/ansible
ca5afc62  2023-04-08 15:01:45  node1.pipo.nl              /home/pipo/ansible
-----------------------------------------------------------------------------
2 snapshots


# restic -r /mnt/node1/restic-repo forget e7be4fe6
-----------------------------------------------------------------------------
ca5afc62  2023-04-08 15:01:45  node1.pipo.nl              /home/pipo/ansible
-----------------------------------------------------------------------------
1 snapshots

now really remove them
#  restic -r /mnt/node1/restic-repo prune   
```

{{< button relref="/" >}}Go Home{{< /button >}}

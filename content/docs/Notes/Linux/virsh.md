---
title: "virsh"
weight: 3
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---



# Life backup vm


## start the vm

```
$ virsh start vm1
Domain 'vm1' started
```

## Enumerate the disks in use

```
$ virsh domblklist vm1
 Target   Source
--------------------------------------
 vda      /var/lib/libvirt/images/vm1.qcow2
```

## Begin backup

```
$ virsh backup-begin vm1
Backup started
```

## Check job status

```
$ virsh domjobinfo vm1
Job type:         None
```

## Check completion

```
$ virsh domjobinfo vm1 --completed
Job type:         Completed
Operation:        Backup
Time elapsed:     183          ms
File processed:   39.250 MiB
File remaining:   0.000 B
File total:       39.250 MiB
```

## Check backup

```
$ ls -lash /var/lib/libvirt/images/vm1.qcow2*
15M -rw-r--r--. 1 qemu qemu 15M May 10 12:22 vm1.qcow2
21M -rw-------. 1 root root 21M May 10 12:23 vm1.qcow2.1620642185
```



# Snapshots

List snapshots
  - virsh snapshot-list runner.qrom.nl
  - sudo qemu-img snapshot -l runner.qrom.nl.qcow2


Create snapshot
   -  virsh snapshot-create-as --domain runner.qrom.nl --name "dosnappie" --description "the best snap" --atomic


Info snapshot
   -  virsh snapshot-info --domain runner.qrom.nl  --snapshotname dosnappie


Revert snapshot
    - virsh snapshot-revert --domain runner.qrom.nl --snapshotname dosnappie


Delete snapshot
   - virsh snapshot-delete runner.qrom.nl --snapshotname dosnappie



## External snapshots

 [external snapshots](https://fabianlee.org/2021/01/10/kvm-creating-and-reverting-libvirt-external-snapshots/ )

 [snapshots](https://kashyapc.fedorapeople.org/virt/lc-2012/snapshots-handout.html)

   - virsh snapshot-create-as runner.qrom.nl --name snappieh  ( gives runner.qrom.nl.snappieh )
   - virsh snapshot-create-as runner.qrom.nl --name snappiehz  ( gives runner.qrom.nl.snappiehz )
   - sudo qemu-img info /var/lib/libvirt/images/runner.qrom.nl.snappiehz -U --backing-chain

If you want to remove a part of the chain you can do this with blockcommit.
Its not possible to delete the past part. That you should do to delete the vm and recreate it with the base image.

   - virsh blockcommit runner.qrom.nl vda --base /var/lib/libvirt/images/runner.qrom.nl.qcow2 --top /var/lib/libvirt/images/runner.qrom.nl.qcow2/snappieh --wait --verbose
     ( now sn1 is gone from the chain )


## External snapshot with own choose of diskname


Create snapshot external
   - virsh snapshot-create-as --domain runner.qrom.nl snap1 snap1-descrip --disk-only --diskspec vda,snapshot=external,file=/tmp/sn1.qcow --atomic
   - virsh snapshot-create-as --domain runner.qrom.nl snap2 snap2-descrip --disk-only --diskspec vda,snapshot=external,file=/tmp/sn2.qcow --atomic
   - virsh domblklist runner.qrom.nl  ( /tmp/sn2.qcow )
   - virsh snapshot-list runner.qrom.nl   

   - virsh blockcommit runner.qrom.nl vda --base /var/lib/libvirt/images/runner.qrom.nl.qcow2 --top /tmp/sn1.qcow --wait --verbose  ( now sn1 is gone from the chain )

now list the chain of /tmp/sn2.qcow and we see sn1 is removed/committed.

   - sudo qemu-img info /var/lib/libvirt/images/runner.qrom.nl.pipo -U --backing-chain


## Create fast VM with backing file

You need a base VM ( called golden-image )

Then create "new VM disk" based on this golden-image:
  - sudo qemu-img create -f qcow2 -b rhel9-golden.qcow2 -F qcow2 apollo.vda.x86_64.qcow2
  - sudo qemu-img create -f qcow2 -b rhel9-golden.qcow2 -F qcow2 saturn.vda.x86_64.qcow2


### Example install virt with backing file

```
 virt-install \
--name apollo \
--ram 4096 \
--os-variant generic \
--disk=apollo.qcow2,bus=virtio,format=qcow2 \
--import
```



{{< button relref="/" [class="..."] >}}Get Home{{< /button >}}


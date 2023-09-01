---
title: "dracut"
weight: 2
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

![Dracut](/images/dracut.jpg)


# Dracut

Used to create a new initrd or to change the initrd.

Linux manual online voor [dracut](https://man7.org/linux/man-pages/man8/dracut.8.html)  

Fedore: [dracut problems](https://docs.fedoraproject.org/en-US/quick-docs/debug-dracut-problems/)
Fedore: [grub2](https://docs.fedoraproject.org/en-US/fedora/latest/system-administrators-guide/kernel-module-driver-configuration/Working_with_the_GRUB_2_Boot_Loader/)

## onder Linux

- lsinitrd
- dracut -force   \#  maak generic initramfs

Summary of dracut kernel command line options

A selection of the most common debugging related dracut options:
rd.shell

Drop to a shell, if the initramfs fails.
rd.debug

Set \-x for the dracut shell.  

    rd.break=[cmdline|pre-udev|pre-trigger|initqueue|pre-mount|mount|pre-pivot|cleanup]

Set udev to loglevel info
rd.udev.debug

Set udev to loglevel debug

## wat kan je allemaal doen

With rd.break you can stop on several levels in the initrd/initramfs
e.g.: **rd.break=mount**  
Now is / gemount mounted on /sysroot as read only  
no sys proc dev  
no /boot  

So what to do?  

    mount -o remount,rw /sysroot
    mount --bind /sys /sysroot/sys
    mount --bind /proc /sysroot/proc
    mount --bind /dev /sysroot/dev
    blkid om te zien waar /boot is
    mount /dev/sdax /sysroot/boot
    chroot /sysroot

Now you can use dracut to build a new initrd.
    dracut foobar.img

You can also adjust /etc/default/grub or passwd 

This can be used when starting and stop in boot menu.

# grub

See blog [rescue a non booting grub](https://www.linuxfoundation.org/blog/blog/classic-sysadmin-how-to-rescue-a-non-booting-grub-2-on-linux)

Stop booting in menu and press 'c'  

Now you are in:
grub>

There is also a grub rescue mode who is limited in use.

    grub> set pager=1
    
    grub> ls
    (hd0) (hd0,msdos2) (hd0,msdos1)
    
    grub> ls (hd0,1)
    grub> cat (hd0,1)/etc/issue
    grub> ls (hd0,gpt2)/

## booting from grub

Some systems do not use prefix /boot

    grub> set root=(hd0,1)
    grub> linux /boot/vmlinuz-3.13.0-29-generic root=/dev/sda1
    grub> initrd /boot/initrd.img-3.13.0-29-generic
    grub> boot

In grub-rescue things are used lke this:

    grub rescue> set prefix=(hd0,1)/boot/grub
    grub rescue> set root=(hd0,1)
    grub rescue> insmod normal
    grub rescue> normal
    grub rescue> insmod linux
    grub rescue> linux /boot/vmlinuz-3.13.0-29-generic root=/dev/sda1
    grub rescue> initrd /boot/initrd.img-3.13.0-29-generic
    grub rescue> boot

## Making Permanent Repairs

See: How do it use [ip command](https://www.cyberciti.biz/faq/linux-ip-command-examples-usage-syntax/)

When you have successfully booted your system, run these commands to fix GRUB permanently:

    $ update-grub

## netwerk activeren

    $ ip a add 192.168.192.91/24 dev eth0
    $ ip link set dev eth0 up
    $ ip route add default via 192.168.192.1 dev eth0

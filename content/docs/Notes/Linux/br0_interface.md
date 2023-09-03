---
title: "br0 interface"
weight: 3
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---


![bridger](/images/bridge.jpg)

--- 

## Install bridge interface

Example on how to install on **eno1** en bridge interface **br0**



```
nmcli con add con-name br0 type bridge ifname br0 ip4 192.168.192.88/24 gw4 192.168.192.1
nmcli con add con-name br0-slave type bridge-slave ifname eno1 master br0
nmcli con modify br0 ipv4.dns 192.168.192.1 ipv4.dns-search example.nl
 
nmcli c down br0
nmcli c up br0
nmcli c up br0-slave 
ping 192.168.192.1
```
 

iproute2 commands
=================

## 1. Add and delete vlan

Add new vlan 200 to interface eth0,
```shell
$ ip link add link eth0 name eth0.200 type vlan id 200

$ ifconfig eth0.200 192.168.1.10 netmask 255.255.255.0

$ route add default gw 192.168.1.1

$ ip link del eth0.200
```

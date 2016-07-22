iptables
===================

1. list chains, verbosely

  ```shell
  $ iptables -L -v
  Chain INPUT (policy ACCEPT 3267K packets, 598M bytes)
   pkts bytes target     prot opt in     out     source               destination
      0     0 ACCEPT     udp  --  virbr0 any     anywhere             anywhere             udp dpt:domain
      0     0 ACCEPT     tcp  --  virbr0 any     anywhere             anywhere             tcp dpt:domain

  Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
   pkts bytes target     prot opt in     out     source               destination
      0     0 ACCEPT     all  --  virbr0 virbr0  anywhere             anywhere
      0     0 REJECT     all  --  virbr0 any     anywhere             anywhere             reject-with icmp-port-unreachable

  Chain OUTPUT (policy ACCEPT 1267K packets, 298M bytes)
   pkts bytes target     prot opt in     out     source               destination
      0     0 ACCEPT     udp  --  any    virbr0  anywhere             anywhere             udp dpt:bootpc
  ```

1. Clear all configured rules

  ```shell
  $ iptables -F # or iptables --flush
  ```

1. Policy chain default behavior (actions)

  * ACCEPT
  * DROP
  * REJECT - same as DROP, but will send back an error

  ```shell
  $ iptables -L | grep policy
  Chain INPUT (policy ACCEPT)
  Chain FORWARD (policy ACCEPT)
  Chain OUTPUT (policy ACCEPT)

  $ iptables --policy INPUT ACCEPT
  $ iptables --policy OUPUT DROP
  $ iptables --policy FORWARD REJECT
  ```

1. Blocking specific connections

  ```shell
  # drop all traffic from 10.10.10.10
  # -A: append to INPUT chain
  # -j: jump to the specified target(action)
  $ iptables -A INPUT -s 10.10.10.10 -j DROP

  # drop by src range
  $ iptables -A INPUT -s 10.10.10.10/24 -j DROP

  # control by port
  $ iptables -A INPUT -p tcp --dport ssh -s 10.10.10.10 -j DROP

  # by connection states
  # -m: load a module
  $ iptables -A INPUT -p tcp --dport ssh -s 10.10.10.10 -m state --state NEW,ESTABLISHED -j ACCEPT
  $ iptables -A OUTPUT -p tcp --sport 22 -d 10.10.10.10 -m state --state ESTABLISHED -j ACCEPT
  $ iptables -A INPUT -p tcp --dport 6881:6890 -j ACCEPT # by port range

  # by mac-address
  $ iptables -A INPUT -s 192.168.0.4 -m mac --mac-source 00:50:8D:FD:E6:32 -j ACCEPT
  ```

1. Save settings to file

  ```shell
  $ iptables-save
  ```



# Reference
 1. [The Beginner's Guide to iptables - the Linux Firewall](http://www.howtogeek.com/177621/the-beginners-guide-to-iptables-the-linux-firewall/)
 1. [CentOS wiki: HOWTO - IPTables](https://wiki.centos.org/HowTos/Network/IPTables)
 1. [Ubuntu wiki: HOWTO - IPTables](https://help.ubuntu.com/community/IptablesHowTo)

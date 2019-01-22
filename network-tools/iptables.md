iptables
===================

# 1. List Rules
1. list chains, verbosely

    ```shell
    $ sudo iptables -L -v
    Chain INPUT (policy ACCEPT 3267K packets, 598M bytes)
     pkts bytes target     prot opt in     out     source       destination
        0     0 ACCEPT     udp  --  virbr0 any     anywhere     anywhere       udp dpt:domain
        0     0 ACCEPT     tcp  --  virbr0 any     anywhere     anywhere       tcp dpt:domain

    Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
     pkts bytes target     prot opt in     out     source       destination
        0     0 ACCEPT     all  --  virbr0 virbr0  anywhere     anywhere
        0     0 REJECT     all  --  virbr0 any     anywhere     anywhere       reject-with icmp-port-unreachable

    Chain OUTPUT (policy ACCEPT 1267K packets, 298M bytes)
     pkts bytes target     prot opt in     out     source       destination
        0     0 ACCEPT     udp  --  any    virbr0  anywhere     anywhere       udp dpt:bootpc
    ```

1. List active iptables

    * `-S`: list rules in the selected chain. If no chain is selected, all chains are printed like iptables-save.
    * `-L`: list rules as tables.

    ```shell
    $ sudo iptables -S
    -P INPUT ACCEPT
    -P FORWARD ACCEPT
    -P OUTPUT ACCEPT
    -N DOCKER
    -N DOCKER-ISOLATION
    -A INPUT -i virbr0 -p udp -m udp --dport 53 -j ACCEPT
    -A INPUT -i virbr0 -p tcp -m tcp --dport 53 -j ACCEPT
    -A INPUT -i virbr0 -p udp -m udp --dport 67 -j ACCEPT
    -A INPUT -i virbr0 -p tcp -m tcp --dport 67 -j ACCEPT
    -A FORWARD -j DOCKER-ISOLATION
    -A FORWARD -o docker0 -j DOCKER
    -A FORWARD -o docker0 -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
    -A FORWARD -i docker0 ! -o docker0 -j ACCEPT
    ```

    List specific chain, see the difference of `-S` and `-L`:
    ```shell
    $ sudo iptables -S INPUT
    -P INPUT ACCEPT
    -A INPUT -i virbr0 -p udp -m udp --dport 53 -j ACCEPT
    -A INPUT -i virbr0 -p tcp -m tcp --dport 53 -j ACCEPT
    -A INPUT -i virbr0 -p udp -m udp --dport 67 -j ACCEPT
    -A INPUT -i virbr0 -p tcp -m tcp --dport 67 -j ACCEPT

    $ sudo iptables -L INPUT -v
    Chain INPUT (policy ACCEPT 16M packets, 3705M bytes)
     pkts bytes target     prot opt in     out     source               destination
     0     0 ACCEPT     udp  --  virbr0 any     anywhere             anywhere             udp dpt:domain
     0     0 ACCEPT     tcp  --  virbr0 any     anywhere             anywhere             tcp dpt:domain
     0     0 ACCEPT     udp  --  virbr0 any     anywhere             anywhere             udp dpt:bootps
     0     0 ACCEPT     tcp  --  virbr0 any     anywhere             anywhere             tcp dpt:bootps
    ```
    output with `-S` looks just like the commands used to create them. Prefix with
    `iptable` of each line will result to the real commands.

# 2. Add Rules
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

# 3. Delete Rules
1. Flush/Clear rules

    ```shell
    $ iptables -F       # clear all chains
    $ iptables -F INPUT # clear chain INPUT

    $ iptables -t nat -F # flush table `nat`
    $ iptables -X        # delete all non-default chains
    ```

1. Delete rules

    Deleting a rule from a chain is much like adding it, just replace `-A` with `-D`:
    ```shell
    # block ICMP (ping) packets from 10.10.10.10, ping will fail
    $ iptables -A INPUT -s 10.10.10.10 -p icmp -j DROP
    $ iptables -L INPUT
    Chain INPUT (policy ACCEPT)
    target     prot opt source               destination
    ACCEPT     udp  --  anywhere             anywhere             udp dpt:domain
    ACCEPT     tcp  --  anywhere             anywhere             tcp dpt:domain
    ACCEPT     udp  --  anywhere             anywhere             udp dpt:bootps
    ACCEPT     tcp  --  anywhere             anywhere             tcp dpt:bootps
    DROP       icmp --  10.10.10.10

    # remove the rule, then ping will be ok again
    $ iptables -D INPUT -s 10.10.10.10 -p icmp -j DROP
    Chain INPUT (policy ACCEPT)
    target     prot opt source               destination
    ACCEPT     udp  --  anywhere             anywhere             udp dpt:domain
    ACCEPT     tcp  --  anywhere             anywhere             tcp dpt:domain
    ACCEPT     udp  --  anywhere             anywhere             udp dpt:bootps
    ACCEPT     tcp  --  anywhere             anywhere             tcp dpt:bootps
    ```

1. **Delete rule by line-number**

    A more convenient way to remove a rule is to specify its `line-number`:
    ```shell
    $ iptables -L INPUT --line-numbers
    Chain INPUT (policy ACCEPT)
    num  target     prot opt source               destination
    1    ACCEPT     udp  --  anywhere             anywhere             udp dpt:domain
    2    ACCEPT     tcp  --  anywhere             anywhere             tcp dpt:domain
    3    ACCEPT     udp  --  anywhere             anywhere             udp dpt:bootps
    4    ACCEPT     tcp  --  anywhere             anywhere             tcp dpt:bootps

    # delete number-2 rule
    $ iptables -D INPUT 2
    ```

# 4. Reset Rule Statistics

1. clear counters

    `-Z` will clear the (ingress/egress) counters for rules.

    ```shell
    # clear counters for all chains
    $ sudo iptables -Z

    # clear counters for INPUT chain
    $ sudo iptables -Z INPUT

    # clear counters for rule 2 (--line-numbers) INPUT chain
    $ sudo iptables -Z INPUT 2
    ```

# 5. Save and Read Configuration Files
1. Save settings to file

    ```shell
    $ iptables-save
    ```



# Reference
 1. [The Beginner's Guide to iptables - the Linux Firewall](http://www.howtogeek.com/177621/the-beginners-guide-to-iptables-the-linux-firewall/)
 1. [CentOS wiki: HOWTO - IPTables](https://wiki.centos.org/HowTos/Network/IPTables)
 1. [Ubuntu wiki: HOWTO - IPTables](https://help.ubuntu.com/community/IptablesHowTo)
 1. [How to List and Delete iptables Firewall Rules](https://www.digitalocean.com/community/tutorials/how-to-list-and-delete-iptables-firewall-rules)
 1. [Stackoverflow: How to Remove Specific Rules From iptables](http://stackoverflow.com/questions/10197405/how-can-i-remove-specific-rules-from-iptables)

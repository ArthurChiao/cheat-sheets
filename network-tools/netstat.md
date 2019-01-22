netstat
==================

1. basic

    | command | effects |
    | :--------- | :-------- |
    | -t | tcp connections |
    | -u | udp connections |
    | -n | numeric values |
    | -l | show only listening sockets |
    | -p | show the PID and name of the program to which each socket belongs |
    | -s | show summary for each protocol |
    | -e/--extend | display additional info, e.g. user. Far more addtional info with `-ee` |

    Summary for each protocol:
    ```shell
    $ netstat -s
    Ip:
      1289619 total packets received
      0 forwarded
      0 incoming packets discarded
      1283187 incoming packets delivered
      520522 requests sent out
    Tcp:
      7778 active connections openings
      1 passive connection openings
      0 failed connection attempts
      0 connection resets received
      11 connections established
      572073 segments received
      536368 segments send out
      15 segments retransmited
      0 bad segments received.
      39 resets sent
    Udp:
      219 packets received
      43 packets to unknown port received.
      0 packet receive errors
      219 packets sent
    ```

    Show TCP connections:
    ```shell
    $ netstat -t
    Active Internet connections (w/o servers)
    Proto Recv-Q Send-Q Local Address           Foreign Address         State
    tcp        0      0 compute-2.mt:47926 controller-21.matr:amqp ESTABLISHED
    tcp        0      0 compute-2.mt:47132 controller-21.matr:amqp ESTABLISHED
    tcp        0      0 compute-2.mt:40482 10.18.12.34:9696        TIME_WAIT
    ```

    More info with `-e`:

    ```cpp
    $ netstat -t -e
    Active Internet connections (w/o servers)
    Proto Recv-Q Send-Q Local Address           Foreign Address         State       User       Inode
    tcp        0    208 10.18.12.34:ssh          10.16.56.78:27261      ESTABLISHED root       39063862
    tcp        0      0 localhost:50225         localhost:epmd          ESTABLISHED rabbitmq   12447
    tcp6       0      0 localhost:epmd          localhost:50225         ESTABLISHED rabbitmq   10739
    ```

## Examples
1. list ports/connections opened by a certain process/program

    Suppose you started a program:
    ```shell
    $ python consumer.py
    ```

    How to list all the ports/connections this program opens?

    First, use `ps` to get the process ID:

    ```shell
    $ ps -ef | grep publisher
    root     15225  5615 12 12:15 pts/16   00:14:15 python consumer.py
    ```

    Then, list all connections with `netstat` and fileter the result with process ID:

    ```shell
    $ netstat -tep | grep 15225
    tcp        0     28 192.168.1.10:36578 192.168.1.11:amqp ESTABLISHED root       97845485    155225/python

    # or
    $ netstat --all --program | grep 15225
    ```

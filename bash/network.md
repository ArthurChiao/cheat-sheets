network tools/commands
========================

1. netstat

  Print network connections, routing tables, interface statistics,
  masquerade connections, and multicast memberships

  | command | effects |
  | :--------- | :-------- |
  | -t | tcp connections |
  | -u | udp connections |
  | -n | numeric values |
  | -l | show only listening sockets |
  | -p | show the PID and name of the program to which each socket belongs |

  ```shell
  # show all tcp and udp connections, grep `80` in result
  netstat -lntup | grep 80
  ```

1. lsof

  查看所有打开的套接字和文件

  ```shell
  $ lsof
  vim       31901 31902           cloud  mem       REG                8,1   728344    67998 /usr/lib/x86_64-linux-gnu/libgdk-x11-2.0.so.0.2400.23
  vim       31901 31902           cloud  mem       REG                8,1  4428264    67997 /usr/lib/x86_64-linux-gnu/libgtk-x11-2.0.so.0.2400.23
  vim       31901 31902           cloud  mem       REG                8,1   149120    59177 /lib/x86_64-linux-gnu/ld-2.19.so
  vim       31901 31902           cloud  mem       REG                8,1    26258    59108 /usr/lib/x86_64-linux-gnu/gconv/gconv-modules.cache
  vim       31901 31902           cloud    0u      CHR              136,5      0t0        8 /dev/pts/5
  vim       31901 31902           cloud    1u      CHR              136,5      0t0        8 /dev/pts/5
  vim       31901 31902           cloud    2u      CHR              136,5      0t0        8 /dev/pts/5
  vim       31901 31902           cloud    3r     FIFO                0,8      0t0 42356884 pipe
  vim       31901 31902           cloud    4w     FIFO                0,8      0t0 42356884 pipe
  ```

1. [simple web server in two lines](http://www.slideshare.net/mestery/openstack-neutron-tutorial)

  ```shell
  MYIP=$(ifconfig eth0 | grep 'inet addr' | awk -F: '{print $1}' | awk '{print $2}')
  while true; do echo -e "HTTP/1.0 200 OK\r\n\r\nWelcome to $MYIP" | sudo nc -l -p 80; done)]
  ```
  the first command get the ip address on `eth0`, the second command starts a
  web server listening on port 80.
  
  `nc`: arbitrary TCP and UDP connections and listens. `-l` used to specify
  that `nc` should listen for an incoming connection rather than initiate a
  connection to a remote host.

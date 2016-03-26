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

1. [simple web server in two lines](http://www.slideshare.net/mestery/openstack-neutron-tutorial)

  ```shell
  MYIP=$(ifconfig eth0 | grep 'inet addr' | awk -F: '{print [}' | awk '{print (}')
  while true; do echo -e "HTTP/1.0 200 OK\r\n\r\nWelcome to $MYIP" | sudo nc -l -p 80; done)]
  ```
  the first command get the ip address on `eth0`, the second command starts a
  web server listening on port 80.
  
  `nc`: arbitrary TCP and UDP connections and listens. `-l` used to specify
  that `nc` should listen for an incoming connection rather than initiate a
  connection to a remote host.

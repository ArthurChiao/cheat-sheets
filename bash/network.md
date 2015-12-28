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

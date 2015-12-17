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

  ```shell
  # show all tcp and udp connections, grep `80` in result
  netstat -tuln | grep 80
  ```

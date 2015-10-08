1. pgrep, pkill
pgrep, pkill - look up or signal processes based on name and other attributes

```shell
pgrep -u root sshd # list the processes called sshd AND owned by root

pgrep -u root, deamon # list the processes owned by root OR daemon

pkill sshd # kill process named sshd
```

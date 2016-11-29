linux permissions
=================

1. users - list all logged in users

  ```shell
  $ users
  root root root root stack stack stack stack stack stack stack
  ```

1. id - show user id and group id

  ```shell
  $ id
  uid=0(root) gid=0(root) groups=0(root)

  $ id stack
  uid=1001(stack) gid=1001(stack) groups=1001(stack),1002(libvirtd)
  ```

1. list all ids/users

  ```shell
  $ cut -d: -f1 /etc/passwd
  root
  bin
  daemon
  adm
  lp
  sync
  shutdown
  halt
  mail
  operator
  games
  ftp
  nobody
  avahi-autoipd
  dbus
  polkitd
  tss
  ```

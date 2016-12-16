basic commands
======================

1. `whatis`, `info`, `man`

  show help information of given command
  ```shell
  whatis python # less information
  info python   # more information
  man python    # more information
  ```

1. `which` - shows the full path of (shell) commands

  ```shell
  which python
  ```

1. `rm`

  `rm` support regex:

  ```shell
  $ touch test0 test1 test2
  $ ls
  test0 test1 test2

  $ rm test[0-2]
  $ ls
  ```

1. `ls`

  List the top 4 files that have been changed recently:

  ```shell
  # -t: sort by modification time, newest first
  # --full-time: specify time format for output
  $ ls -t --full-time /var/log | head -5
  total 1920
  -rw-r----- 1 syslog   adm       84501 2016-12-16 11:17:01.579357398 +0800 auth.log
  -rw-r----- 1 syslog   adm        3356 2016-12-16 11:17:01.575357398 +0800 syslog
  -rw------- 1 root     root       3994 2016-12-16 09:01:49.443522932 +0800 conntrackd-stats.log
  drwxr-xr-x 2 root     root       4096 2016-12-16 06:25:01.887714901 +0800 openvswitch
  ```

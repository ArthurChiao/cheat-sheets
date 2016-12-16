bash commands
=============

1. [basic commands](basic.md)

  `whatis`, `info`, `man`, `which`, `rm`, `ls`

1. [file options](file.md)

  `df`, `du`, `rev`, `find`, `tee`, `dd`, `tar`, `rename`

1. [process options](proc.md)

  `pgrep`, `pkill`, `pidof`, `strace`, `ltrace`, `ps`

1. [text processing](text.md)

  `grep`, `tr`, `sed`, `uniq`, `wc`, `basename`, `dirname`, `readlink`

1. [network tools](network.md)

  `netstat`, `lsof`

1. [time utils](time.md)

  `date`

1. [misc commands/tools](misc.md)

  `bind`, `compgen`, `disown`, `hash`, `printenv`

1. [built-in macros](macro.md)

1. [bash mode](bash-mode.md)

1. [permissions](permission.md)


--------------------

# bash resources

1. [Architecture of Open Source Applications: Chapter2 bash](http://www.aosabook.org/en/bash.html)

  `Bash` architecture.

1. [Netflix Tech: Linux Performance Analysis in 60,000 Milliseconds](http://techblog.netflix.com/2015/11/linux-performance-analysis-in-60s.html)

  You login to a Linux server with a performance issue: what do you check in
  the first minute?

  In this post, the Netflix Performance Engineering team will show you the
  first 60 seconds of an optimized performance investigation at the command
  line, using standard Linux tools you should have available.

  ```shell
  uptime
  dmesg | tail
  vmstat 1
  mpstat -P ALL 1
  pidstat 1
  iostat -xz 1
  free -m
  sar -n DEV 1
  sar -n TCP,ETCP 1
  top
  ```

1. [The Art of Command Line](https://github.com/jlevy/the-art-of-command-line)

  **Tutorial on `github` with 21K stars and 2K forks.**

  Chinease version [这篇文章可以帮你掌握命令行的艺术](http://blog.jobbole.com/90364/)

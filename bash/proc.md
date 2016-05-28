**Index**

1. [pgrep, pkill](#pgrep)
1. [pidof](#pidof)
1. [strace](#strace)
1. [ltrace](#ltrace)
1. [ps](#ps)

---------

1. <a name="pgrep">pgrep, pkill</a>

  pgrep, pkill - look up or signal processes based on name and other attributes

  ```shell
  pgrep -u root sshd # list the processes called sshd AND owned by root

  pgrep -u root, deamon # list the processes owned by root OR daemon

  pkill sshd # kill process named sshd
  ```

1. <a name="pifof">pidof</a>

  find the process ID of a running program.
  similar as `ps -e | grep <program>`

  ```shell
  $ pidof docker
  5883 1985

  $ ps -e | grep docker
  1985 ?        00:00:26 docker
  5883 pts/19   00:00:00 docker
  ```

1. <a name="trace">strace</a>

  `strace` - trace system call and signals of the given process/program.

  strace has two modes:

    * trace a process at start up: by prefixing "strace" before your command:
    * trace an existing process: pass process ID with `-p` option

  ```shell
  # trace `ls -lh /var/log/`
  $ strace ls -lh /var/log/

  # trace an existing process
  $ pidof some_server
  17553
  $ strace -p 17553
  ```

  Highly recommend this article: [运维利器：万能的 strace](http://mp.weixin.qq.com/s?__biz=MzA4Nzg5Nzc5OA==&mid=2651659767&idx=1&sn=3c515cb32bcbcafe16c749024d1545ef&scene=0#wechat_redirect)


1. <a name="trace">ltrace</a>

  `ltrace` - a library call tracer (trace userpace libraries, routines)


1. <a name="ps">ps</a>

  report a snapshot of the current processes

  ```shell
  $ ps s # display signal format
   UID   PID          PENDING          BLOCKED          IGNORED           CAUGHT STAT TTY        TIME COMMAND
  1000  3651 0000000000000000 0000000000010000 0000000000380004 000000004b817efb Ss   pts/1      0:00 bash
  1000 16410 0000000000000000 0000000000000000 0000000000380004 000000004b817efb Ss+  pts/8      0:00 -bash
  1000 16463 0000000000000000 0000000000010000 0000000000380004 000000004b817efb Ss   pts/15     0:00 -bash
  1000 16517 0000000000000000 0000000000000000 0000000000081802 0000000188034201 S+   pts/1      0:00 tmux att
  1000 16759 0000000000000000 0000000000000000 0000000000000000 0000000073d3fef9 R+   pts/15     0:00 ps s

  $ kill -l # see which signals your system implements
  1) SIGHUP       2) SIGINT       3) SIGQUIT      4) SIGILL       5) SIGTRAP
  6) SIGABRT      7) SIGBUS       8) SIGFPE       9) SIGKILL     10) SIGUSR1
  11) SIGSEGV     12) SIGUSR2     13) SIGPIPE     14) SIGALRM     15) SIGTERM
  16) SIGSTKFLT   17) SIGCHLD     18) SIGCONT     19) SIGSTOP     20) SIGTSTP
  21) SIGTTIN     22) SIGTTOU     23) SIGURG      24) SIGXCPU     25) SIGXFSZ
  26) SIGVTALRM   27) SIGPROF     28) SIGWINCH    29) SIGIO       30) SIGPWR
  31) SIGSYS      34) SIGRTMIN    35) SIGRTMIN+1  36) SIGRTMIN+2  37) SIGRTMIN+3
  38) SIGRTMIN+4  39) SIGRTMIN+5  40) SIGRTMIN+6  41) SIGRTMIN+7  42) SIGRTMIN+8
  43) SIGRTMIN+9  44) SIGRTMIN+10 45) SIGRTMIN+11 46) SIGRTMIN+12 47) SIGRTMIN+13
  48) SIGRTMIN+14 49) SIGRTMIN+15 50) SIGRTMAX-14 51) SIGRTMAX-13 52) SIGRTMAX-12
  53) SIGRTMAX-11 54) SIGRTMAX-10 55) SIGRTMAX-9  56) SIGRTMAX-8  57) SIGRTMAX-7
  58) SIGRTMAX-6  59) SIGRTMAX-5  60) SIGRTMAX-4  61) SIGRTMAX-3  62) SIGRTMAX-2

  # Retrieve a list of the pids of child processes of the given pid
  $ ps --ppid <pid> -o pid=

  $ ps --ppid 1 -o pid=
  366
  758
  787
  804
  864
  868
  871
  872
  874
  896
  912
  960
  1045
  1165
  2151
  2797
  10442
  18860
  18863
  18866
  ```

----------

# Reference

1. [运维利器：万能的 strace](http://mp.weixin.qq.com/s?__biz=MzA4Nzg5Nzc5OA==&mid=2651659767&idx=1&sn=3c515cb32bcbcafe16c749024d1545ef&scene=0#wechat_redirect)

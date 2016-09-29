**Index**

1. [pgrep, pkill](#pgrep)
1. [pidof](#pidof)
1. [strace](#strace)
1. [ltrace](#ltrace)
1. [ps](#ps)
1. [kill/pkill](#kill)

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

1. <a name="strace">strace</a>

  `strace` - trace system call and signals of the given process/program.

  strace has two modes:

    * trace a process at start up: by prefixing "strace" before your command:
    * trace an existing process: pass process ID with `-p` option

  Each line of the output shows a system call. Examples:

  ```shell
  # trace `ls -lh /var/log/`
  $ strace ls -lh /var/log/

  # trace an existing process
  $ pidof some_server
  17553
  $ strace -p 17553
  ```

  Trace following c program, source file `pid.c`:

  ```c
  #include<stdio.h>
  #include<stdlib.h>
  #include<sys/types.h>
  #include<unistd.h>

  int main(int argc, char *argv[])
  {
    pid_t p = getpid();
    printf("%d\n", p);
    return 0;
  }
  ```

  ```shell
  $ gcc -o pid pid.c

  $ strace ./pid
  execve("./pid", ["./pid"], [/* 22 vars */]) = 0
  brk(0)                                  = 0x1cce000
  access("/etc/ld.so.nohwcap", F_OK)      = -1 ENOENT (No such file or directory)
  mmap(NULL, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x7ff9bf26e000
  access("/etc/ld.so.preload", R_OK)      = -1 ENOENT (No such file or directory)
  open("/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3
  fstat(3, {st_mode=S_IFREG|0644, st_size=38280, ...}) = 0
  mmap(NULL, 38280, PROT_READ, MAP_PRIVATE, 3, 0) = 0x7ff9bf264000
  close(3)                                = 0
  access("/etc/ld.so.nohwcap", F_OK)      = -1 ENOENT (No such file or directory)
  open("/lib/x86_64-linux-gnu/libc.so.6", O_RDONLY|O_CLOEXEC) = 3
  read(3, "\177ELF\2\1\1\0\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\320\37\2\0\0\0\0\0"..., 832) = 832
  fstat(3, {st_mode=S_IFREG|0755, st_size=1845024, ...}) = 0
  mmap(NULL, 3953344, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x7ff9bec88000
  mprotect(0x7ff9bee43000, 2097152, PROT_NONE) = 0
  mmap(0x7ff9bf043000, 24576, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x1bb000) = 0x7ff9bf043000
  mmap(0x7ff9bf049000, 17088, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0x7ff9bf049000
  close(3)                                = 0
  mmap(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x7ff9bf263000
  mmap(NULL, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x7ff9bf261000
  arch_prctl(ARCH_SET_FS, 0x7ff9bf261740) = 0
  mprotect(0x7ff9bf043000, 16384, PROT_READ) = 0
  mprotect(0x600000, 4096, PROT_READ)     = 0
  mprotect(0x7ff9bf270000, 4096, PROT_READ) = 0
  munmap(0x7ff9bf264000, 38280)           = 0
  getpid()                                = 29643
  fstat(1, {st_mode=S_IFCHR|0620, st_rdev=makedev(136, 1), ...}) = 0
  mmap(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x7ff9bf26d000
  write(1, "29643\n", 629643
  )                  = 6
  exit_group(0)                           = ?
  +++ exited with 0 +++
  ```

  [If you have a process that appears stuck, you can strace it and see what
  it might be doing via system calls. When some app is quitting
  unexpectedly without a proper error message, check if a syscall failure
  explains it. You can also use filters, time each call, and so so](http://duartes.org/gustavo/blog/post/system-calls/)

  ```shell
  $ strace -T -e trace=recv curl -silent www.google.com. > /dev/null

  recv(3, "HTTP/1.1 200 OK\r\nDate: Wed, 05 N"..., 16384, 0) = 4164 <0.000007>
  recv(3, "fl a{color:#36c}a:visited{color:"..., 16384, 0) = 2776 <0.000005>
  recv(3, "adient(top,#4d90fe,#4787ed);filt"..., 16384, 0) = 4164 <0.000007>
  recv(3, "gbar.up.spd(b,d,1,!0);break;case"..., 16384, 0) = 2776 <0.000006>
  recv(3, "$),a.i.G(!0)),window.gbar.up.sl("..., 16384, 0) = 1388 <0.000004>
  recv(3, "margin:0;padding:5px 8px 0 6px;v"..., 16384, 0) = 1388 <0.000007>
  recv(3, "){window.setTimeout(function(){v"..., 16384, 0) = 1484 <0.000006>
  ```

1. <a name="ltrace">ltrace</a>

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

  **show process state:**

  ```shell
  $ ps l # show BSD long format
  F   UID   PID  PPID PRI  NI    VSZ   RSS WCHAN  STAT TTY        TIME COMMAND
  0  1000   360  7265  20   0 211036 43348 poll_s Sl+  pts/27     1:17 vim
  0  1000  1578  2758  20   0  24876  5796 n_tty_ Ss+  pts/26     0:00 -bash
  0  1000  5069 15041  20   0 180652 12720 poll_s Sl+  pts/5      0:02 vim midiroute.c
  0  1000  5420  2758  20   0  25772  6812 wait   Ss   pts/28     0:04 -bash
  0  1000  8655  8129  20   0  15800  1200 poll_s S+   pts/3      0:00 tmux a
  ```

  If a process is sleeping, the **WCHAN** column will tell what kernel event
  the process is waiting for.

  The **STAT** column:

  * `s`: this process is a session leader
  * `+`: this process is part of a foreground process group

1. <a name="kill">kill/pkill</a>

  Despite its misleading name, `kill/pkill` is actually a tool to send
  specific signals to a running process - kill the process is actually only
  one of its many functionalities.

  * `kill` - send a signal to a process, specify the **process ID**.
  * `pkill` - send a signal to a process, specify the **process name**.

  see which signals your system implements:
  ```shell
  $ kill -l
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
  ```

  If no signal specified, `kill/pkill` will
  send `SIGTERM` to the process, which asks the process to kill itself.
  However, the process can be set to ignore this signal (through register
  signal handler), so `kill <process id>` does not always kills a process.

  A more bruteforce way to kill a process is by passing `-9` to `kill/pkill`
  which sends `SIGKILL`. Note that this signal will not be sent to the process,
  but to the `init` process - the parent process of all other processes in the
  system (which means an ordinary process can not ignore this signal).
  On receiving this signal, `init` process kills the specified process
  immediatly.

  examples, kill an running process named `apache2`:
  ```shell
  $ ps -e | grep apche2
  24161 ?        00:00:10 apache2

  # send SIGTERM signal to the apache2 process, using kill/pkill
  $ kill 24161 # same as kill -15 24161
  $ pkill apache2 # same as pkill -15 apache2

  # send SIGKILL signal to the apache2 process
  $ kill -9 24161
  $ pkill -9 apache2 # same as pkill -9 apache2
  ```

----------

# Reference

1. [运维利器：万能的 strace](http://mp.weixin.qq.com/s?__biz=MzA4Nzg5Nzc5OA==&mid=2651659767&idx=1&sn=3c515cb32bcbcafe16c749024d1545ef&scene=0#wechat_redirect)
1. [System Calls Make the World Go Round](http://duartes.org/gustavo/blog/post/system-calls/)
1. [谁偷走了你的服务器性能——strace & Ltrace篇](http://rdcqii.hundsun.com/portal/article/597.html)

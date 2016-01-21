**Index**

1. [pgrep, pkill](#pgrep)
1. [strace, ltrace](#trace)
1. [ps](#ps)

<a name="pgrep"></a>
## pgrep, pkill
pgrep, pkill - look up or signal processes based on name and other attributes

```shell
pgrep -u root sshd # list the processes called sshd AND owned by root

pgrep -u root, deamon # list the processes owned by root OR daemon

pkill sshd # kill process named sshd
```

<a name="trace"></a>
## strace, ltrace
`strace` - trace system call and signals

`ltrace` - a library call tracer (trace userpace libraries, routines)


<a name="ps"></a>
## ps
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
```

tty
========

1. [tty](#tty)
1. [stty](#stty)

-------------

1. <a name="tty">tty</a>

  Which terminal we are using:

  ```shell
  $ tty
  /dev/pty/7
  ```

1. <a name="stty">stty</a>

  `stty` - change and print terminal line settings

  ```shell
  $ stty -a # list all settings
  speed 38400 baud; rows 57; columns 184; line = 0;
  intr = ^C; quit = ^\; erase = ^?; kill = ^U; eof = ^D; eol = <undef>; eol2 = <undef>; swtch = <undef>; start = ^Q; stop = ^S; susp = ^Z; rprnt = ^R; werase = ^W; lnext = ^V; flush = ^O;
  min = 1; time = 0;
  -parenb -parodd cs8 -hupcl -cstopb cread -clocal -crtscts
  -ignbrk -brkint -ignpar -parmrk -inpck -istrip -inlcr -igncr icrnl ixon -ixoff -iuclc -ixany -imaxbel iutf8
  opost -olcuc -ocrnl onlcr -onocr -onlret -ofill -ofdel nl0 cr0 tab0 bs0 vt0 ff0
  isig icanon iexten echo echoe echok -echonl -noflsh -xcase -tostop -echoprt echoctl echoke
  ```

  change terminal settings:

  ```shell
  $ stty -F /dev/pty/7 rows 30
  ```

# Reference

1. [The TTY Demystified](http://www.linusakesson.net/programming/tty/index.php)

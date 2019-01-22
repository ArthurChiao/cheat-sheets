misc commands
=====================

1. `bind`

    bind可以很方便地在shell中实现宏或按键的绑定.
    在进行按键绑定的时候，我们需要先获取到绑定按键对应的字符序列。

    `showkey -a` 查看按键对应的字符序列。

    比如获取F12的字符序列：先按下Ctrl+V,然后按下F12 .我们就可以得到F12的字符序列 ^[[24~。


    ```shell
    $ bind '"\e[24~":"date"'
    ```

1. `type`

    ```shell
    $ type ll
    ll is aliased to `ls -alF'

    $ type function
    function is a shell keyword
    ```

1. `alias` - show alias list

    ```shell
    $ alias
    alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'
    alias egrep='egrep --color=auto'
    alias fgrep='fgrep --color=auto'
    alias grep='grep --color=auto'
    alias l='ls -CF'
    alias la='ls -A'
    alias ll='ls -alF'
    alias ls='ls --color=auto'
    ```


1. 打印出所有支持的命令列表

    ```shell
    $ compgen -c
    ```

1. 在不重启机器的条件下，有什么方法可以把所有正在运行的进程移除呢？

    ```shell
    $ disown -r
    ```

1. `hash`

    命令’hash’管理着一个内置的哈希表，记录了已执行过的命令的完整路径, 
    可以打印出所使用过的命令以及执行的次数。

    系统上的$PATH变量包含的路径可能更多，目录中的文件数量也可能会很多。
    于是，遍历这些目录去查询文件名的行为就可能比较耗时。于是bash提供了一种功能，
    就是建立一个bash表，在第一次找到一个命令的路径之后，
    对其命令名和对应的路径建立一个hash索引。这样下次再执行这个命令的时候，
    就不用去遍历所有的目录了，只要查询索引就可以更快的找到命令路
    径，以加快执行程序的速度。

    ```shell
    $ hash
    hits    command
     9    /bin/grep
     1    /usr/bin/basename
     1    /usr/local/bin/pip
 149    /usr/bin/git
    10    /bin/rm
     4    /bin/chmod
     3    /bin/cat
    70    /usr/bin/vim
     7    /usr/bin/sudo
     2    /bin/mv
     2    /usr/bin/python3
     1    /bin/mkdir
     7    /bin/cp
     1    /usr/bin/man
    47    /bin/ls
     1    /usr/bin/find
     8    /usr/bin/python

    $ hash -l
    builtin hash -p /bin/grep grep
    builtin hash -p /usr/bin/basename basename
    builtin hash -p /usr/local/bin/pip pip
    builtin hash -p /usr/bin/git git
    builtin hash -p /bin/rm rm
    builtin hash -p /bin/chmod chmod
    builtin hash -p /bin/cat cat
    builtin hash -p /usr/bin/vim vim
    builtin hash -p /usr/bin/sudo sudo
    builtin hash -p /bin/mv mv
    builtin hash -p /usr/bin/python3 python3
    builtin hash -p /bin/mkdir mkdir
    builtin hash -p /bin/cp cp
    builtin hash -p /usr/bin/man man
    builtin hash -p /bin/ls ls
    builtin hash -p /usr/bin/find find
    builtin hash -p /usr/bin/python python
    ```

1. shellbang

    Bash script must be started with `#!`, and it has to be the **first 2 characters
    of the first line**. It is parsed by the **kernel** (not `shell` itself, and
    shell will ignore any lines started with `#` - including this line) to
    decide which program will be used to execute this script. So, in theory,
    you can put any program in the `shellbang`, e.g.:

    Below `cat.sh` will be executed by `cat`, which prints everything in the file:

    ```shell
    #!/bin/cat

    echo "hello, world"
    ```

    Another example `rm.sh`:

    ```shell
    #!/bin/rm

    echo "hello, world"
    ```
    Try and see what happens!

1. list supported shells of your system

    ```shell
    $ cat /etc/shells
    # /etc/shells: valid login shells
    /bin/sh
    /bin/dash
    /bin/bash
    /bin/rbash
    /usr/bin/tmux
    /usr/bin/screen
    ```

1. print all environment variables

     ```shell
     $ printenv
     ```

------------

## References
1. [10个核心的Linux面试问题与答案](http://www.geekfan.net/8571/)
1. [SHELL编程之执行过程](http://mp.weixin.qq.com/s?__biz=MzIxNDMyODgyMA==&mid=2247483666&idx=1&sn=b3df5f3f8d8803fb88719463388db4ed&scene=0#wechat_redirect)

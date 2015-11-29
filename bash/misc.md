misc commands
=====================

1. `bind`

  bind可以很方便地在shell中实现宏或按键的绑定.
  在进行按键绑定的时候，我们需要先获取到绑定按键对应的字符序列。

  `showkey -a` 查看按键对应的字符序列。

  比如获取F12的字符序列：先按下Ctrl+V,然后按下F12 .我们就可以得到F12的字符序列 ^[[24~。


  ```shell
  bind '"\e[24~":"date"'
  ```

1. 打印出所有支持的命令列表

  ```shell
  compgen -c
  ```

1. 在不重启机器的条件下，有什么方法可以把所有正在运行的进程移除呢？

  ```shell
  disown -r
  ```

1. `hash`

  命令’hash’管理着一个内置的哈希表，记录了已执行过的命令的完整路径, 可以打印出所使用过的命令以及执行的次数。

  ```shell
  hash
  ```

1. `whatis`

  查看一个linux命令的概要与用法

  ```shell
  whatis ls
  whatis man
  ```

------------

## References
1. [10个核心的Linux面试问题与答案](http://www.geekfan.net/8571/)

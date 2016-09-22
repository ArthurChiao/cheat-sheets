linking, loading, inspecting tools
====================

# Index

1. [nm](#nm)
1. [objdump](#objdump)
1. [ldd](#ldd)
1. [inspect memory mapping](#inspect memory mapping)
1. [readelf](#readelf)
1. [ld](#ld)
1. [modinfo](#modinfo)
1. [reference](#reference)

<h2 id="nm">nm - list symbols from object files</h2>
```shell
gcc -c test.c -o test.o
nm test.o
```

`nm` could also list the symbols from **excutables and shared library**:
```shell
gcc test.o -o test

nm test

nm -D libxxx.so # list symbols in libxxx.so
```


<h2 id="objdump">objdump - display information from object files</h2>
```shell
gcc test.o -o test

objdump -D test | less
```


<h2 id="ldd">ldd - show shared library dependencies</h2>
`ldd` lists the shared library dependencies of an excutable file:
```shell
ldd a.out

linux-vdso.so.1 =>  (0x00007fff7fd9b000)
libc.so.6 => /lib64/libc.so.6 (0x0000003f42400000)
lib64/ld-linux-x86-64.so.2 (0x0000003f41c00000)
```

ldd 命令模拟加载可执行程序需要的动态链接库，但并不执行程序，后面的地址部分
表示模拟装载过程中动态链接库的地址。如果尝试多次运行 ldd 命令，
我们会发现每次动态链接库的地址都是不一样的，因为这个地址是动态定位的。
我们平常工作中，如果某一个二进制可执行文件报错找不到某个函数定义，
可以用这个命令检查是否系统丢失或者没有安装某一个动态链接库。



<h2 id="inspect memory mapping">inspect memory mapping</h2>
`cat /proc/<pid>/maps/` where <pid> is the process ID.

```shell
7feeef61f000-7feeef7d4000 r-xp 00000000 fd:01 135891 /lib/x86_64-linux-gnu/libc-2.15.so
7feeef7d4000-7feeef9d3000 ---p 001b5000 fd:01 135891 /lib/x86_64-linux-gnu/libc-2.15.so
7feeef9d3000-7feeef9d7000 r--p 001b4000 fd:01 135891 /lib/x86_64-linux-gnu/libc-2.15.so
7feeef9d7000-7feeef9d9000 rw-p 001b8000 fd:01 135891 /lib/x86_64-linux-gnu/libc-2.15.so
```


<h2 id="readelf">readelf - Displays information about ELF files</h2>
```shell
readelf -d a.out
```


<h2 id="ld">ld - loading tool</h2>
Generate a shared library with `ld`:
```shell
# alternative 1
gcc -fPIC -c -Wall test.c # PIC: Position Independent Code
ld -shared test.o -o libtest.so

# alternative 2
gcc -fPIC -shared -Wall -o libtest.so test.c

# generate shared lib, with specified version
gcc -fPIC -shared -Wall -Wl,-soname,libtest.so.0  -o libtest.so.0.0.0 test.c
```

<h2 id="modinfo">modinfo - show module information</h2>
```shell
$ modinfo openvswitch
filename:       /lib/modules/3.13.0-32-generic/kernel/net/openvswitch/openvswitch.ko
license:        GPL
description:    Open vSwitch switching datapath
srcversion:     47D3079FB6731A4B46CED6E
depends:        libcrc32c,vxlan,gre
intree:         Y
vermagic:       3.13.0-32-generic SMP mod_unload modversions
signer:         Magrathea: Glacier signing key
sig_key:        5E:3C:0F:xx:9E:84:F1:6D:A7:C7
sig_hashalgo:   sha512
```

<h2 id="lsmod">lsmod, insmod, modprobe</h2>

* lsmod - list all installed modules
* insmod - install module
* modprobe - install module, and all its dependent modules

```shell
$ lsmod
Module                  Size  Used by
binfmt_misc            17468  1
xfrm_user              31045  1
xfrm_algo              15394  1 xfrm_user
8021q                  28895  0
garp                   14384  1 8021q
mrp                    18778  1 8021q
veth                   13331  0
xt_addrtype            12635  2
dm_thin_pool           46897  1
dm_persistent_data     61525  1 dm_thin_pool
dm_bufio               27502  1 dm_persistent_data
dm_bio_prison          15501  1 dm_thin_pool
ipt_MASQUERADE         12880  5
iptable_nat            13011  1
nf_nat_ipv4            13263  1 iptable_nat
nf_nat                 21841  3 ipt_MASQUERADE,nf_nat_ipv4,iptable_nat
nf_conntrack_ipv4      15012  3
nf_defrag_ipv4         12758  1 nf_conntrack_ipv4
```

It reads contents from `/proc/modules`.

```shell
$ cat /proc/modules
binfmt_misc 17468 1 - Live 0x0000000000000000
xfrm_user 31045 1 - Live 0x0000000000000000
xfrm_algo 15394 1 xfrm_user, Live 0x0000000000000000
8021q 28895 0 - Live 0x0000000000000000
garp 14384 1 8021q, Live 0x0000000000000000
mrp 18778 1 8021q, Live 0x0000000000000000
veth 13331 0 - Live 0x0000000000000000
xt_addrtype 12635 2 - Live 0x0000000000000000
dm_thin_pool 46897 1 - Live 0x0000000000000000
dm_persistent_data 61525 1 dm_thin_pool, Live 0x0000000000000000
dm_bufio 27502 1 dm_persistent_data, Live 0x0000000000000000
dm_bio_prison 15501 1 dm_thin_pool, Live 0x0000000000000000
ipt_MASQUERADE 12880 5 - Live 0x0000000000000000
iptable_nat 13011 1 - Live 0x0000000000000000
```


# Reference
-------------
1. [高级语言的编译：链接及装载过程介绍](http://tech.meituan.com/linker.html)
1. [Linux动态库相关知识整理](http://zkt.name/linuxgong-xiang-ku-de-chuang-jian-yu-shi-yong/?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io)

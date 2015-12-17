**Index**

1. [df: filesystem disk usage](#df)
1. [du: disk usage](#du)
1. [rev: reverse text lines](#rev)
1. [find: find a file and execute actions on results](#find)
1. [file: show file info](#file)
1. [dd: copy and convert file](#dd)
1. [tar: create/extract archives](#tar)

<a name="df"></a>
## df - report file system disk space usage
```shell
# show disk usage, in human readable (-h) format:
$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2       907G  111G  750G  13% /
none            4.0K     0  4.0K   0% /sys/fs/cgroup
udev            4.8G  4.0K  4.8G   1% /dev
tmpfs           984M  1.3M  983M   1% /run
none            5.0M     0  5.0M   0% /run/lock
none            4.9G  106M  4.7G   3% /run/shm
none            100M   48K  100M   1% /run/user
/dev/sda1       511M  3.4M  508M   1% /boot/efi
```

<a name="du"></a>
## du - estimate disk (space) usage of a folder or file
```shell
du -sh <file or folder>

# exmaples
du -sh . # total disk usage of current folder

du -sh * # disk usage of each files in current folder

du -sh ./log # disk usage of ./log folder

# useful shortcut
alias lss='du -sh .'

lss # same as 'du -sh .'
```

<a name="rev"></a>
## rev - reverse lines of a file or files
```shell
cat TODO.md

1. network optimization: classid in linux network

rev TODO.md

krowten xunil ni dissalc :noitazimitpo krowten .1
```

<a name="find"></a>
## find and remove all `*.pyc` files, recursively
```shell
find . -name "*.pyc" -exec rm -f {} \; # remove file

find . -name "*.pyc" -exec git rm -f {} \; # remove from git repo

# 将当前目录下的所有权变更为arthur
# {}是一个特殊的字符串，对于每一个匹配的文件，{}会被替换成相应的文件名
find . -type f -user root -exec chown arthur {} \;

# copy all found files to another folder
find . -type f -mtime +10 -name "*.txt" -exec cp {} OLD \;

# 如果需要后续执行多个命令，可以将多个命令写成一个脚本。然后 -exec 调用时执行脚本
-exec ./task.sh {} \;
```

count how many files in current folder:
```shell
find . | wc -l

# list all files in current dir, and number them
ls | cat -n # `-n` number all output lines

    1  LICENSE
    2  README.md
    3  bash
    4  compile
    5  git
    6  profiling.md
    7  tmux.md
```

```shell
# find all .txt
find . -name "*.txt"

# find all files except .txt
find . ! -name "*.txt"

# specify search depth
find . -maxdepth 1 -type f
```

find by ***time/size/permission/***:

| command | effects |
| :------ | :------------ |
| find . -atime 7 -type f | 最近`第7天`被访问过的所有文件 |
| find . -atime -7 -type f | 最近`7天内`被访问过的所有文件 |
| find . -atime +7 -type f | `7天前`被访问过的所有文件 |
| find . -type f -size +2k | 寻找大于2k的文件 |
| `find . -size 0 | xargs rm -f &` | remove zero size files |
| find . -type f -perm 644 | 找具有可执行权限的所有文件 |
| find . -type f -user arthur | find all files owned by `arthur` |


<a name="file"></a>
## show file info, such as file type
```shell
file README.md

# find all executables in current dir
ls -lrt | awk '{print $9}'|xargs file|grep  ELF| awk '{print (}'|tr -d ':')
```


<a name="dd"></a>
## convert and copy a file.
Copy a file, converting and formatting according to the operands.

Example, generate 1GB test file with random data:
```shell
dd if=/dev/urandom of=testdata bs=1M count=1024

# if: read from file instead of stdin
# of: write to file instead of stdout
# bs: read and write BYTES bytes at a time (also see ibs=,obs=)
# count: copy only N input blocks
```

<a name="tar"></a>
## create/extract archives
`Tar` comes from `Tape Archiver`, it is a POSIX standard.
`tar` only packs files (result in `.tar` files), if you want compress them,
you need to specify a compression method, e.g, `bzip2` (`.tar.bz2`),
`gzip` (`.tar.gz`).

```shell
# put all files in `/home/xxx/testdir/` into a new created archive, and
# compress it with `gzip` format
tar pczf test.tar.gz /home/xxx/testdir

# `p` - preserve file attributes and priviledges
# `c` - create new file
# `z` - compress with gzip
# `f` - create new archive file, otherwise the output will be `stdout`


# extract files
tar xzvf test.tar.gz
# 'x' - extract
# 'z' - gzip compressed
# 'v' - verbose
# 'f' - read from a file (`test.tar.gz`)
```

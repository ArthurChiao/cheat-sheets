**Index**

1. [df: filesystem disk usage](#df)
1. [du: disk usage](#du)
1. [rev: reverse text lines](#rev)
1. [find: find a file and execute actions on results](#find)
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

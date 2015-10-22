**Index**

1. [du](#du)
1. [rev](#rev)
1. [find](#find)

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

text processing
=================

Index:

1. [grep](#grep)
1. [tr](#tr)
1. [sed](#sed)
1. [uniq](#uniq)
1. [sort](#sort)
1. [wc](#wc)
1. [basename/dirname/readlink](#basename_dirname_readlink)
1. [awk](#awk)

---------------

1. <a name="grep">`grep`</a>

  | Command  |  Function |
  | :-------- |  :--------- |
  | -A n   | 保留匹配行上面n行上下文 |
  | -B n   | 保留匹配行下面n行上下文 |
  | -R     | recursively into sub-folders |
  | -v     | find lines that do not contain the text specified |
  | -i     | case insensitive |
  | -n     | show line number of matched lines |
  | -l     | only show matched file names |
  | `--include=*.cpp` | only search in `.cpp` files |
  | `--exclude=*.cpp` | skip `.cpp` files |
  | `--exclude-dir=tests` | skip `tests` directory in current folder |

  ```shell
  # grep word `session`, retain uppper and down context (each 2 lines)
  $ grep -A 2 -B 2 -R session *

  # find lines do not include `session` in a.txt
  $ grep -v session a.txt

  # find text lines containing `AAA` but not containing `BBB`, count lines
  $ cat -v record.log | grep AAA | grep -v BBB | wc -l

  # regular expression: find lines DO NOT contain character `e`
  $ cat test.txt | grep -v 'e.*'

  $ grep -R --include *.cpp keyword

  $ grep -R --exclude=*.svg --exclude=*.js 400 # grep `400`
  ```

  For a project under-developing, you could create a `grep.sh` like this:

  ```shell
  #!/bin/sh

  grep -R --color=always --exclude=tags --exclude-dir=tests \
      --exclude-dir=datapath-windows \
      --exclude-dir=ovn \
      --exclude-dir=xenserver \
      "$@"
  ```

  and grep something like the following, which filters out lots of
  items matched in un-interested files/dirs:

  ```shell
  $ ./grep.sh ofproto *
  ```

  **grep also supports Chinese**:

  ```shell
  $ grep -R "您没有权限来上传" *
  apps/files/l10n/zh_CN.js:    "You don’t have permission to upload or create files here" : "您没有权限来上传湖州哦和创建文件",
  apps/files/l10n/zh_CN.json:    "You don’t have permission to upload or create files here" : "您没有权限来上传湖州哦和创建文件",
  ```

  **Perfect!**

  **count lines of effective Python code**, ignore blank lines and comment lines (start with `#`):

  ```shell
  $ grep -v '^ *\(#.*\)\?$' test.py | wc -l
  ```

  Combining with `sed`, substitute all `abcd` with `efgh`:

  ```shell
  $ grep -R -l abcd * # only show matched files

  $ grep -R -l abcd * | xargs sed -i 's/abcd/efgh/g' # substitute
  ```

1. <a name="tr">`tr` - 可以完成简单的字符转换任务</a>

  ```shell
  # 把 grephelp.txt 文件转换为全文大写
  cat grephelp.txt | tr '[:lower:]' '[:upper:]'
  ```
  简而言之，tr 的工作就是把第一个集合中的字符转换为第二个集合中的相应的字符。

  **Generate random string** (characters including \_A-Z-a-z-0-9):

  ```shell
  $ cat /dev/urandom | tr -dc _A-Z-a-z-0-9 | head -c 16
  I05sa1DMEkK5cgx6
  ```

1. <a name="sed">`sed`</a>

  tr 命令的应用场景非常受限，如果希望进行更加灵活的模式替换，我们还有 sed（也就是 stream editor，流编辑器）。
  ```shell
  # 把文件中所有的 "find" 文本替换为 "search"
  # `s` - substitute
  # `g` - substitute all matched in the line
  sed "s/find/search/g" grephelp.txt

  # sed 默认把处理结果打印到标准输出，我们可以通过重定向把处理结果转储到一个新文件中，或者使用选项 -i 把结果直接写回原文件
  sed -i "s/find/search/g" grephelp.txt

  # 把文件中所有的数字 n 替换为 "--n--" 的形式
  sed -E "s/([0-9]+)/--\1--/g" grephelp.txt

  # get current branch name
  MY_CURRENT_BRANCH=$(cat .git/HEAD | sed 's/ref: //g')
  ```

  **Using search results:**
  ```shell
  $ cat test.txt
  5555551214
  6665551216
  777555121

  $ sed -e 's/^[[:digit:]][[:digit:]][[:digit:]]/(&)/g' test.txt
  (555)5551214
  (666)5551216
  (777)5551217

  # -e: use multiple sed commands
  $ sed -e 's/^[[:digit:]]\{3\}/(&)/g'  \
      -e 's/)[[:digit:]]\{3\}/&-/g' phone.txt
  (555)555-1214
  (666)555-1216
  (777)555-1217
  ```

  ----------

  **Replacing macro in C file**

  Some C/C++ projects use special MACROs to generate cross-platform code, e.g.
  a macro `PJ_DEF` defines something like this:

  ```c
  #ifdef WIN_DLL
  #define PJ_DEF __dllexport__
  #else
  #define PJ_DEF // do nothing
  #endif
  ```

  Then a function definition looks like this:
  ```c
  PJ_DEF(pj_status_t) pj_fun_a(int a, int b) {
      // function body
  }
  ```

  This is an excellent idea, however, it prohibits `ctags` from generating the
  proper tags file, and thus can not find the definition as you jumping code.
  If just intend to browsing the code, you could use `sed` to remove those
  "annoying" `PJ_DEF`s:

  ```shell
  $ cd project_dir

  $ find . -name *.c | xargs sed -i 's/^PJ_DEF//g'

  $ ctags -R --languages=C,C++ *
  ```

  Now ctags works OK!


1. <a name="uniq">`uniq` - remove repeated lines</a>

  ```shell
  uniq a.txt # print a.txt, omit repeated lines

  uniq -d a.txt # print only the repeated lines

  uniq -c a.txt # list the repeatitions of each distinct line

  # c is a union b
  cat a b | sort | uniq > c

  # c is a intersect b
  cat a b | sort | uniq -d > c

  # c is set difference a - b
  cat a b b | sort | uniq -u > c
  ```

1. <a name="sort">`sort` - sort text line</a>
  ```shell
  sort report.txt # sort by alphabet order

  sort -u report.txt # unique and sort, remove repeated lines
  ```

1. <a name="wc">`wc` - word count</a>

  ```shell
  `-c` - count bytes
  `-m` - count chars
  `-w` - count words
  `-l` - count lines

  # see how many unique lines in a.txt
  uniq a.txt | wc -l
   ```

1. <a name="basename_dirname_readlink">`basename`, `dirname`, `readlink`</a>

  `basename` - trip directory and suffix from filenames
  ```shell
  $ basename /usr/bin/sort
  sort

  $ basename include/stdio.h .h
  stdio

  # -s: with suffix
  $ basename -s .h include/stdio.h
  stdio

  # -a: multiple arguments, each treat as a file
  $ basename -a any/str1 any/str2
  str1
  str2
  ```

  `dirname` - strip last component from file name
  ```shell
  $ dirname /home/client.c
  home
  ```

  `readlink` - print resolved symbolic links or canonical file names
  ```shell
  $ readlink -f /usr/bin/python
  /usr/bin/python2.7
  ```

1. <a name="awk">`awk`</a>

  Remove all duplicated lines in a file ([Blog](http://www.infoworld.com/article/2985804/linux/remember-sed-awk-linux-admins-should.html)):

  ```shell
  $ awk '!seen[$0]++' file
  ```

  This answer is the most concise and simplest solution to the problem.
  It's the same effect with the following code, which is more readable:

  ```shell
  $ awk '{ if (!seen[$0]) print $0; seen[$0]++ }'
  ```

# Reference
1. [使用 Linux/Unix 进行文本处理](https://linux.cn/article-6611-1.html)
1. [[译] awk & sed ，一个老派系统管理员的基本素养](https://linux.cn/article-6881-1.html)

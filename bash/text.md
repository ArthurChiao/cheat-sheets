text processing
=================

1. `grep`

  | Command  |  Function |
  | :-------- |  :--------- |
  | -A n   | 保留匹配行上面n行上下文 |
  | -B n   | 保留匹配行下面n行上下文 |
  | -R     | recursively into sub-folders |
  | -v     | find lines that do not contain the text specified |

  ```shell
  # grep word `session`, retain uppper and down context (each 2 lines)
  grep -A 2 -B 2 -R session *

  # find lines do not include `session` in a.txt
  grep -v session a.txt

  # find text lines containing `AAA` but not containing `BBB`, count lines
  cat -v record.log | grep AAA | grep -v BBB | wc -l
  ```

1. `tr` - 可以完成简单的字符转换任务

  ```shell
  # 把 grephelp.txt 文件转换为全文大写
  cat grephelp.txt | tr '[:lower:]' '[:upper:]'
  ```
  简而言之，tr 的工作就是把第一个集合中的字符转换为第二个集合中的相应的字符。

1. `sed`

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
  ```

1. `uniq` - remove repeated lines
  ```shell
  uniq a.txt # print a.txt, omit repeated lines

  uniq -d a.txt # print only the repeated lines

  uniq -c a.txt # list the repeatitions of each distinct line
  ```

1. `sort` - sort text line
  ```shell
  sort report.txt # sort by alphabet order

  sort -u report.txt # unique and sort, remove repeated lines
  ```

1. `wc` - word count
   ```shell
   `-c` - count bytes
   `-m` - count chars
   `-w` - count words
   `-l` - count lines

   # see how many unique lines in a.txt
   uniq a.txt | wc -l
   ```


# Reference
1. [使用 Linux/Unix 进行文本处理](https://linux.cn/article-6611-1.html?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io)

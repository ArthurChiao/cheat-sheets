## Pattern Matching

Two consecutive asterisks (`**`) in patterns matched against full pathname
may have special meaning:

- A leading `**` followed by a slash means ***match in all directories***.

  ```shell
  **/foo # matches file or directory `foo` anywhere, the same as pattern `foo`
         # 匹配所有foo文件(夹)

  **/foo/bar # matches file or directory `bar` anywhere that is directly under directory `foo`.
             # 匹配所有foo文件夹下的bar文件(夹)
  ```

- A trailing `/**` ***matches everything inside***.

  ```
  abc/** # matches all files inside directory `abc`, relative to the
         # location of the .gitignore file, with infinite depth.
         # 匹配abc文件夹下所有文件
  ```

- A slash followed by two consecutive asterisks then a slash ***matches
zero or more directories***.

  ```
  a/**/b # matches `a/b`, `a/x/b`, `a/x/y/b` and so on.
  ```

Other consecutive asterisks are considered invalid.


# Reference
1. [git-scm.com](http://git-scm.com/docs/gitignore)

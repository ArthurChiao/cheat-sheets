git submodule
==============

1. <a name="init">git submodule init</a>

  submodules are meant for different projects you would like to make part of
  your source tree, while the history of the two projects still stays
  completely independent and you cannot modify the contents of the submodule
  from within the main project.

  ```shell
  $ git submodule init
  $ git submodule update
  ```

  Example git submodule file: `.gitmodules` in ownCloud:
  ```
  [submodule "doc/ocdoc"]
      path = doc/ocdoc
      url = https://github.com/owncloud/documentation
  [submodule "binary"]
      path = binary
      url = git://github.com/owncloud/owncloud-client-binary.git
  ```
  This will create two directories `doc/ocdoc` and `binary`,
  and git clone the specified repos into the dir, respectively.

1. <a name="pull_latest">pull latest changes</a>

  ```shell
  $ git submodule foreach git pull origin master
  ```

  see [stackoverflow](http://stackoverflow.com/questions/1030169/easy-way-pull-latest-of-all-submodules) for more info.


# Reference


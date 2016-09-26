basic commands
======================

1. `whatis`, `info`, `man`

  show help information of given command
  ```shell
  whatis python # less information
  info python   # more information
  man python    # more information
  ```

1. `which` - shows the full path of (shell) commands

  ```shell
  which python
  ```

1. `rm`

  `rm` support regex:

  ```shell
  $ touch test0 test1 test2
  $ ls
  test0 test1 test2

  $ rm test[0-2]
  $ ls
  ```

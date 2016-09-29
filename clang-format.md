clang-format
=============

1. A basic configuration file for C/C++ files

  File `.clang-format`, put it at the root dir of source code:

  ```yaml
  BasedOnStyle: LLVM
  IndentWidth: 4
  BreakBeforeBraces: Linux
  AllowShortIfStatementsOnASingleLine: false
  IndentCaseLabels: true
  ```

  Run:

  ```shell
  # apply to specific file, -i: inplace edit
  $ clang-format -i test.c

  # apply to source directory, recursivly
  $ clang-format -i .

  # apply to only .c files
  $ find . -name '*.c' | xargs clang-format -i
  ```

# References
1. [CLANG-FORMAT STYLE OPTIONS](http://clang.llvm.org/docs/ClangFormatStyleOptions.html)

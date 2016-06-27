ctags
============

1. basic usage
  ```shell
  # generate tags for all files in current and all child directories:
  $ ctags -R

  $ ctags -V [options] # verbose, debug mode
  ```

2. exclude specific files
  ```shell
  $ ctags --exclude=*.html --exclude=*.js ./*
  ```

3. generate only for specific languages
  ```shell
  $ ctags --list-languages # show all supported languages
  Ant
  Asm
  Asp
  Awk
  Basic
  BETA
  C
  C++
  C#
  Cobol
  CSS
  DosBatch
  Eiffel
  Erlang
  Flex
  Fortran
  HTML
  Java
  JavaScript
  Lisp
  Lua
  Make
  MatLab
  OCaml
  Pascal
  Perl
  PHP
  Python
  REXX
  Ruby
  Scheme
  Sh
  SLang
  SML
  SQL
  Tcl
  Tex
  Vera
  Verilog
  VHDL
  Vim
  YACC

  # only include PHP files, note that language name is case-sensitive
  $ ctags -R --languages=PHP *

  # .h files are classified into C++ files, see `man ctags` for details
  # so we need to add `C++` to `--languages` option for C projects,
  # otherwise `.h` files will not be included
  $ ctags -R --languages=C,C++ *
  ```

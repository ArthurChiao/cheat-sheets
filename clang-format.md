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

    [.clang-format for 3.5](.clang-format-3.5)

1. clang-format off for a piece of code

    `// clang-format off` or `/* clang-format off */` in source code could be
    understood by clang-format:

    ```cpp
    int formatted_code;
    // clang-format off
        void    unformatted_code  ;
    // clang-format on
    void formatted_code_again;
    ```

# References
1. [CLANG-FORMAT STYLE OPTIONS](http://clang.llvm.org/docs/ClangFormatStyleOptions.html)

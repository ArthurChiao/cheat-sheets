openSUSE commands
===================

1. delete all `snapshot` files

    openSUSE uses `snapper` to take snapshots of ***btrfs*** partitions. These
    are large files, in `/.snapshots/` folder, and more importantly, you can not
    remove them even with root previlege (`sudo`).

    Instead, you have to use `snapper delete` command:

    ```shell
    $ snapper list

    $ snapper delete <N1> - <N2>
    ```

    ```shell
    $ for i in `seq 1 999`; do snapper delete $i; done
    ```

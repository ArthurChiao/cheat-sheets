git push
===================

1. push existing repo to new repo, keep all histories

    ```shell
    $ git clone <existing_repo>
    $ cd <existing_repo>
    $ git push --mirror <new_repo>
    ```

1. delete remote branch

    ```shell
    $ git push origin --delete <branch>
    ```

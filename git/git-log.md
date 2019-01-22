git log [others]
==============

Index:

1. [General](#git_log)
1. [Exclude Merges in Git Log](#no_merges)
1. [View Commit Differences between Branches](#commit_diff_between_brs)

------------

1. <a name="git_log">git log</a>

    ```shell
    # Show recent commit histories that impose changes on `filepath`
    # 列出最近的commit history中,影响`filepath`的commits
    $ git log -- <filepath>

    # Show recent commit histories that impose changes on `filepath`, and all the changes
    # 列出最近的commit history中,影响`filepath`的commits, and all the changes
    $ git log -p --<filepath>

    # Show file changes between `commit1` and `commit2`
    # 两次commit之间某文件的改动
    $ git diff <commit1>:<filepath> <commit2>:<filepath>
    ```

    Show commit history in pretty will format:

    ```shell
    $ git log --oneline --graph --all --decorate
    *   194b962 (origin/master, origin/HEAD, master) Merge branch 'develop': update cheat sheets
    |\
    | * 8adcc14 (HEAD, develop) update builtin.md
    | * d596482 update cheat sheets
    |/
    * cc2df9d update cheat sheets
    * 715dd48 update README.md
    * 7d606f3 update builtin commands in cheat sheets
    * f9b9eb5 update README.md
    * 5b34613 update cheat-sheets: relativenumber and indent
    * e928a14 update README: add compile vim from source for centos
    * a768de1 add update.sh

    $ git log --graph --all --decorate
    *   commit 194b9620221bcbd95ffd114d0f30a471ed3dc81d (origin/master, origin/HEAD, master)
    |\  Merge: cc2df9d 8adcc14
    | | Author: arthurchiao <arthurchiao@hotmail.com>
    | | Date:   Mon Jul 11 10:05:41 2016 +0800
    | |
    | |     Merge branch 'develop': update cheat sheets
    | |
    | * commit 8adcc148bf8aa2bb33d98a8904554420a55606cd (HEAD, develop)
    | | Author: arthurchiao <arthurchiao@hotmail.com>
    | | Date:   Sun Jul 10 09:40:43 2016 +0800
    | |
    | |     update builtin.md
    | |
    | * commit d596482319f966f279055ea39c38e82206e3be2b
    |/  Author: arthurchiao <arthurchiao@hotmail.com>
    |   Date:   Fri Jul 8 18:43:40 2016 +0800
    |
    |       update cheat sheets
    |
    * commit cc2df9de1b7433164b4ebacec2a6d8880662e439
    | Author: arthurchiao <arthurchiao@hotmail.com>
    | Date:   Thu Jul 7 16:23:23 2016 +0800
    |
    |     update cheat sheets
    |
    * commit 715dd48c81c51c4b42085e585ec7f87d8fe43578
    | Author: arthurchiao <arthurchiao@hotmail.com>
    | Date:   Tue Jul 5 13:09:03 2016 +0800
    |
    |     update README.md
    |
    * commit 7d606f3aab0b36ba60f28112b6cebb4aa809553a
    | Author: arthurchiao <arthurchiao@hotmail.com>
    | Date:   Tue Jul 5 12:34:49 2016 +0800
    |
    |     update builtin commands in cheat sheets
    |
    ```

1. <a name="no_merges">Exclude merges in commits</a>

    In large projects, there will be a robot program (e.g. jenkins) who runs the
    regression test and merges the code automatically with new commits.
    It is annoying to list these commits when you'd like to see the real changes,
    the `--no-merges` option excludes these commits from `log history`:

    ```shell
    $ git log --no-merges
    ```

    more info on [stackoverflow](http://stackoverflow.com/questions/8527139/showing-commits-made-directly-to-a-branch-ignoring-merges-in-git).

1. <a name="commit_diff_bewteen_brs">Commit difference between branches</a>

    Show commit differences between branch `master` and branch `stable/mitaka`:
    ```shell
    $ git cherry -v master stable/mitaka
    - cc275e4975450947fa9d9e55ef42475a25bf611d Linux Bridge: Add mac spoofing filtering to ebtables
    - cd77e8b837556c96cb0a3ad7480d6dc85df3834e LinuxBridge agent's QoS driver bw limit for egress traffic
    + bd61bec9491af22cf6f2c2915057a16cbd65ad09 Support interface drivers that don't support mtu parameter for plug_new
    + d7dc90946407d27eec9063f05f33e3f4888ad395 OVS: Add mac spoofing filtering to flows
    + 6964cdd3cd041ff1d635a99c158f574ef4c094a3 Updated from global requirements
    - eca893be5b770c41cfc570dc016a41c30c2cdf23 Preserve backward compatibility with OVS hybrid plugging
    + 64bddf0d0e2c9b8feddaeaf6126b2b7009f11b83 Imported Translations from Zanata
    ```


EXAMPLES (*from `git log --help`*)

* `git log v2.6.12.. include/scsi drivers/scsi`

    Show all commits since version v2.6.12 that changed any file in the
    include/scsi or drivers/scsi subdirectories

* `git log --since="2 weeks ago" -- gitk`

    Show the changes during the last two weeks to the file gitk.
    The "--" is necessary to avoid confusion with the branch named gitk

* `git log --name-status release..test`

    Show the commits that are in the "test" branch but not yet in the
    "release" branch, along with the list of paths each commit modifies.

* `git log --follow builtin-rev-list.c`

    Shows the commits that changed builtin-rev-list.c, including those commits
    that occurred before the file was given its present name.

* `git log --branches --not --remotes=origin`

    Shows all commits that are in any of local branches but not in any of
    remote tracking branches for origin (what you have that origin doesn't).

* `git log master --not --remotes=*/master`

    Shows all commits that are in local master but not in any remote
    repository master branches.

* `git log -p -m --first-parent`

    Shows the history including change diffs, but only from the "main branch"
    perspective, skipping commits that come from merged branches,
    and showing full diffs of changes introduced by the merges.
    This makes sense only when following a strict policy of merging all topic
    branches when staying on a single integration branch.

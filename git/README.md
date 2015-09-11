EXAMPLES (*from `git log --help`*)

`git log --no-merges`

Show the whole commit history, but skip any merges

`git log v2.6.12.. include/scsi drivers/scsi`

Show all commits since version v2.6.12 that changed any file in the include/scsi or drivers/scsi subdirectories

`git log --since="2 weeks ago" -- gitk`

Show the changes during the last two weeks to the file gitk. The "--" is necessary to avoid confusion with the branch named gitk

`git log --name-status release..test`

Show the commits that are in the "test" branch but not yet in the "release" branch, along with the list of paths each commit modifies.

`git log --follow builtin-rev-list.c`

Shows the commits that changed builtin-rev-list.c, including those commits that occurred before the file was given its present name.

`git log --branches --not --remotes=origin`

Shows all commits that are in any of local branches but not in any of remote tracking branches for origin (what you have that origin doesn't).

`git log master --not --remotes=*/master`

Shows all commits that are in local master but not in any remote repository master branches.

`git log -p -m --first-parent`

Shows the history including change diffs, but only from the "main branch" perspective, skipping commits that come from merged branches, and showing full diffs of changes
introduced by the merges. This makes sense only when following a strict policy of merging all topic branches when staying on a single integration branch.


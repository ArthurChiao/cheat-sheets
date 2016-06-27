
Index:

1. [git log](git-log.md)
1. [git push](git-push.md)
1. [git pull](git-pull.md)
1. [git ignore](git-ignore.md)

------------

## github上fork别人项目后如何与源项目保持同步

Fork `sjtu-medialab/mass` to `arthurchiao/mass`. When `sjtu-medialab/mass` is changed,
i want to pull and rebase the change to `arthurchiao/mass`.

```shell
git clone https://arthurchiao/github.com/arthurchiao/mass.git

cd mass

# add upstream, the name (upstream_medialab) is arbitrary
git remote add upstream_medialab https://github.com/sjtu-medialab/mass.git

# assume on master branch
git pull upstream_medialab master

# if no conflicts, the changes will be rebased onto your code
# push changes to your own repo (https://github.com/arthurchiao/mass.git)
git push origin master
```

## Handle `pull request` and merge code in command line
If you do not want to use the merge button or an automatic merge cannot be
performed, you can perform a manual merge on the command line.

Step 1: From your project repository, check out a new branch and test the changes.
```shell
git checkout -b ArthurChiao-master master
git pull https://github.com/ArthurChiao/mass.git master
```

Step 2: Merge the changes and update on GitHub.
```shell
git checkout master
git merge --no-ff ArthurChiao-master
git push origin master
```

## git clone
```shell
# --depth <depth> Create a shallow clone with a history truncated to the specified number of revisions.
git clone --depth 1 https://github.com/imatix/zguide.git
```

## git clean
git-clean - Remove untracked files from the working tree.

Cleans the working tree by recursively removing files that are not under
version control, starting from the current directory.
```shell
git clean [-d] [-f] [-i] [-n] [-q] [-e <pattern>] [-x | -X] [--] <path>…
```

## remove local/remote branches
```
# remove local branch
git branch --delete --force <branchName>
git branch -D <branchName>

# remove remote branch
git push origin --delete <branchName>
```

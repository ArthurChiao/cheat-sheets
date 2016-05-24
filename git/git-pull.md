1. fetch all remote branches

  ```shell
  $ git branch --list # show local branches
  $ git branch --list --all # show all (local/remote) branches

  # checkout to branch `stable-2.2` from remotes
  $ git checkout -b stable-2.2 remotes/origin/stable-2.2
  ```

  fetch all branches from remote:
  ```shell
  $ git branch -r | grep -v '\->' | while read remote; do git branch --track "${remote#origin/}" "$remote"; done
  $ git fetch --all
  $ git pull --all
  ```

  [reference](http://stackoverflow.com/questions/10312521/how-to-fetch-all-git-branches) from stackoverflow


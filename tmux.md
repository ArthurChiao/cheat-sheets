tmux commands
===============

**Index:**

1. [Basic Shell Commands](#tmux_shell_commands)
1. [Help](#tmux_help)
1. [Session Commands](#tmux_session_commands)
1. [Windows & Panels Commands](#tmux_windows_panels_commands)
1. [Search in Output Window](#tmux_search)
1. [Other Commands](#tmux_other_commands)

------------------

`<leader>` key: default `ctl+b`, I like to bind it to `ctl+j`

1. <a name="tmux_shell_commands">basic tmux commands in shell</a>
  ```shell
  tmux # create new session
  tmux new -s <session name> # create new session, specify name
  # e.g. create and delete sessions
  tmux new -s session_1 # create new session, session name `session_1`
  tmux kill-session -t session_1 # kill `session_1`
  
  tmux ls # list all sessions
  
  tmux att # attach existing session
  tmux a -t <session name> # attach existing session
  
  tmux kill-session -t <session name> # delete specified session
  ```

1. <a name="tmux_help">help</a>
  ```shell
  <leader> ?
  
  <leader> :list-keys # show key bindings
  
  <leader> :list-commands # show commands
  ```

1. <a name="tmux_session_commands">basic session commands</a>
  ```shell
  <leader> :kill-session # delete session
  
  <leader> :kill-server # delete all sessions
  
  <leader> d # log out session temporarily (session is still there in background)
  ```

1. <a name="tmux_windows_panels_commands">windows and panels</a>

  One `session` contains one or multiple `windows`, one `window` can be split
  into many `panels`.
  
  ```shell
  <leader> c # create new window
  <leader> & # delete window
  
  <leader> p # previous window
  <leader> n # next window
  <leader> <N> # jump to window N, where 0 <= N <=9
  <leader> ' # (single quote) select windows by index
             # for those windows with index > 9, jump to them with this command
  
  <leader> , # rename window
  
  <leader> f # search in multiple windows
  
  
  <leader> - # split panel horizontally (my customed binding)
  <leader> | # split panel vertically (my customed binding)
  <leader> x # delete panel
  
  # move between panels
  <leader> o # move sequentially between panels
  <leader> h # move to left panel (my customed binding)
  <leader> j # move to bottom panel (my customed binding)
  <leader> k # move to up panel (my customed binding)
  <leader> l # move to right panel (my customed binding)
  
  # adjust panel size
  <leader> H # enlarge current panel to left (my customed binding)
  <leader> J # enlarge current panel to bottom (my customed binding)
  <leader> K # enlarge current panel to up (my customed binding)
  <leader> L # enlarge current panel to right (my customed binding)
  
  <leader> z # maximize/restore current panel
  
  # move panel
  <leader> { # move panel to left/up
  <leader> } # move panel to right/bottom
  
  <leader> + whitespace # change panel layout
  <leader> ctrl+o # move panel sequentially
  ```

1. <a name="tmux_search">Search in Output Window</a>
  ```shell
  <leader> [ # enter history buffer
  ctl + r # search in window
  ```

1. <a name="tmux_other_commands">others</a>
  ```shell
  <leader> [ # enter copy mode
  
  <leader> t # show current time
  ```

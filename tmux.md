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

`<leader>` key: default `ctl-b`, but I prefer to bind it to `ctl-j`, because
`j` is the key that your finger rests at, thus this binding doesn't hurts your
(left) fingers too much.

1. <a name="tmux_shell_commands">basic tmux commands in shell</a>
  ```shell
  $ tmux                       # create new session
  $ tmux new -s <session name> # create new session, specify name

  # e.g. create and delete sessions
  $ tmux new -s session_1          # create new session, session name `session_1`
  $ tmux kill-session -t session_1 # kill `session_1`
  
  $ tmux ls # list all sessions
  
  $ tmux a                   # attach existing session
  $ tmux a -t <session name> # attach existing session
  
  $ tmux kill-session -t <session name> # delete specified session
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
  # window
  <leader> c # create new window
  <leader> & # delete window
  
  <leader> p # previous window
  <leader> n # next window
  <leader> <N> # jump to window N, where 0 <= N <=9
  <leader> , # rename window
  
  <leader> - # split panel horizontally (my customed binding)
  <leader> | # split panel vertically (my customed binding)
  <leader> x # delete panel
  
  # move between panes
  <leader> o # move sequentially between panels
  <leader> h # move to left pane (my customed binding)
  <leader> j # move to bottom pane (my customed binding)
  <leader> k # move to up pane (my customed binding)
  <leader> l # move to right pane (my customed binding)
  
  # adjust pane size
  <leader> z # maximize/restore current pane
  <leader> H # enlarge current pane to left (my customed binding)
  <leader> J # enlarge current pane to bottom (my customed binding)
  <leader> K # enlarge current pane to up (my customed binding)
  <leader> L # enlarge current pane to right (my customed binding)

  # move pane
  <leader> { # move pane to left/up
  <leader> } # move pane to right/bottom
  
  <leader> whitespace # change pane layout
  <leader> ctl-o # move pane sequentially
  ```

  Advanced:

  ```shell
  # window
  <leader> . # prompt for an index, move current window to there (change window index)
  <leader> w # list windows list, choose window interactively (move up/down with `ctl-p`/`ctl-n`)
  <leader> ' # (single quote) select windows by index
             # for those windows with index > 9, jump to them with this command
  
  # pane
  <leader> ; # move to the previous active pane
  <leader> ! # break current pane out, to a new window
  ```

1. <a name="tmux_search">Search in Output Window</a>
  ```shell
  <leader> [ # enter copy mode, history buffer
  <leader> ] # paste
  ```

1. <a name="tmux_other_commands">others</a>
  ```shell
  <leader> t # show current time
  ```

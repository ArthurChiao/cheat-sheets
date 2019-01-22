tmux commands
===============

**Index:**

1. [Tmux Sessions](#tmux_commands)
1. [Help Within Tmux](#tmux_help)
1. [Windows & Panels Commands](#tmux_windows_panels_commands)
1. [Search in Output Window](#tmux_search)
1. [Other Commands](#tmux_other_commands)

------------------

`<leader>` key: default `ctl-b`, but I prefer to bind it to `ctl-j`, because
`j` is the key that your finger rests at, thus this binding doesn't hurts your
(left) fingers too much.

## 1 <a name="tmux_commands">Tmux Session</a>

Create, list, attach, tmux sessions from Shell:

```shell
$ tmux                        # create new session
$ tmux new -s <name>          # create new session, specify session name
$ tmux ls                     # list all sessions
$ tmux a                      # attach most recently dettached session
$ tmux a -t <name>            # attach specified session
$ tmux kill-session -t <name> # delete specified session

# e.g. create and delete sessions
$ tmux new -s s1            # create new session, session name `s1`
$ tmux kill-session -t s1   # kill `s1`
```

kill or dettach tmux session from within tmux window:

```shell
<leader> :kill-session # delete session

<leader> :kill-server # delete all sessions

<leader> d # dettach session (session is still there in background)
```

## 2 <a name="tmux_help">Help Within Tmux</a>

```shell
<leader> ?
```

In a tmux window/pane, stroke `<leader> :` will prompt up a tmux command line
bar, you could type built-in commands in it (support TAB completion):

```shell
<leader> :list-keys # show key bindings

<leader> :list-commands # show commands
```

## 3 <a name="tmux_windows_panels_commands">Windows and Panes</a>

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

## 4 <a name="tmux_search">Search in Output Window</a>

```shell
<leader> [ # enter copy mode, history buffer
<leader> ] # paste
```

## 5 <a name="tmux_other_commands">Others</a>

* `<leader> t` - show current time
* `<leader> :set synchronize-panes [on|off]` - excute same commands in multiple panes

### installation

  sudo apt-get install tmux

### Usage

At first, type `tmux` in command line prompt to lauch tmux, then using the
following key combination to control the session. More info to check `man tmux`

  ctrl-b %      split the current pane into two, top and bottom.

  ctrl-b "      split the current pane into two, left and right.

  ctrl-b x      kill the current pane.

  ctrl-b &      kill the current window.

  ctrl-b c      create a new window.

         d      Detach the current client.

         f      Prompt to search for text in open windows.

         i      Display some information about the current window.

         l      Move to the previously selected window.

         n      Change to the next window.

         o      Select the next pane in the current window.

         p      Change to the previous window.

         q      Briefly display pane indexes.

### commands

Detach a client after, run the command below to activate the client.

  tmux attach

Attach to an session available when tmux is started. very excellent!

  tmux attach-session

Attach to a specific client, for example, client 1

```
tmux a -t 1
```


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

### command line

# tmux shortcuts & cheatsheet

start new:

  tmux

start new with session name:

  tmux new -s myname

attach:

  tmux a  #  (or at, or attach)

attach to named:

  tmux a -t myname

list sessions:

  tmux ls

kill session:

  tmux kill-session -t myname

Kill all the tmux sessions:

  tmux ls | grep : | cut -d. -f1 | awk '{print substr($1, 0, length($1)-1)}' | xargs kill 


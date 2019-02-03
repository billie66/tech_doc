## change view explorer keyboard shortcut

Code -> Preferences -> Keyboard Shortcuts

find the view explorer command, then open keybindings.json and edit it, add the following lines to the array

```
  {
    "key": "alt+cmd+e",
    "command": "workbench.view.explorer"
  }
```


## File Utils extension

use File Utils extension to manage files

* shift+cmd+p open command palette, and select `File:`
* type proper command to operate file, and press `Enter` to confirm

There is a little inconvenient that this tool can only delete recently used file.


## some common used keyboard shortcuts

* shift+cmd+x open extensions marketplace
* option+cmd+n create a new file
* option+cmd+e open file explorer

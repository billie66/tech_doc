## change view explorer keyboard shortcut

Code -> Preferences -> Keyboard Shortcuts

find the view explorer command, then open keybindings.json and edit it, add the following lines to the array

```
  {
    "key": "alt+cmd+e",
    "command": "workbench.view.explorer"
  }
```

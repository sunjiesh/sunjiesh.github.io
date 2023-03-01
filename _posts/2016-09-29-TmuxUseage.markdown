---
layout: post
title:  "Tmux使用"
date:   2016-09-29 16:34:50 +0800
categories: Linux
---

### creates a new tmux session

```shell
tmux new -s session_name
```

### attach session

```shell
tmux attach -t session_name
```

### list session

```shell
tmux ls
```

### open new tab

```shell
hit Ctrl + B and then C
```

### Moving among tabs
```shell
To move among these tabs hit the following keys:

    Ctrl + B and then n to go to the next tab on the right
    Ctrl + B and then p to go to the previous tab on the left
    Ctrl + B and then {number} to go to the tab with number equal to {number} (e.g. 0 to go to the first tab)
```

### Closing a tab
```shell
To close a tab, move to it and then hit Ctrl + B and then x and then hit y and Enter to confirm closing of this tab.
```


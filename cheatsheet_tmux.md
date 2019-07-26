# tmux 

.tmux.conf : https://github.com/alasta/config/blob/master/.tmux.conf

### Start basic sesison
```
tmux 
```

### Start New Session
```
tmux new -s SessionName
```

### Attach Session
```
tmux attach : Attach to last session
```
  
### Attach to Session Name  
```
tmux a -t SessionName
OR
tmux attach -t SessionName
```

### Kill Session Name
```
tmux kill-session -t mysession
```

### Kill all sessions
```
tmux kill-session -a
```

### List session
```
tmux ls
```


### Crontrol key

Control x : C^x 

### Switch Windows
Shift arrow Left/Right

### Switch Panes
Control arrow

### Fx Keys
```
F1  : Move current window to left  
F2  : Move current window to right  
F3  : Choose window  
F4  : Choose session  
F5  : Rename window name  
F6  : Split vertical window  
F7  : Split horizontal window   
F8  : Save history to file
F9  : Open new window  
F10 : Enable/disable sync command to all panes
F11 : Close current window  
F12 : Close all window
```
  
### Sessions  
```
C^x :new<CR>  : New session
C^x s         : List sessions
C^x $         : Display or rename session name
C^x (         : Previous session
C^x )         : Next session
C^x L         : Switch to last session
```
  
### Windows (tabs)
```
C^x c : Open new window
C^x , : Rename current window name
C^x n : Go to next window
C^x p : Go to previous window
C^x l : Go to last window
C^x w : List/switch windows
C^x f : Find window with pattern (in name or content)
C^x 1 : Switch to window 1 (or other number)
C^x ' : Select window by number
C^x . : Change window number

C^x & : Ask to kill current window

C^x :joinp -s :3  : Move window 3 into a new pane in the current window
C^x :joinp -t :1  : Move the current pane into a new pane in window 1
C^x :join -v -s 1.0 -p 25 : Add window 1 pane 0 in current window with hplit vertical at 25%
```
  
### Panes (splits)
```
C^x % : Horizontal split
C^x " : Vertical split
C^x o : Switch panes
C^x q : Show pane numbers
C^x space : Toggle panes
C^x { : Move to left pane
C^x } : Move to right pane
C^x C^o : Rotate pane up
C^x Alt^o : Rotate pane down
C^x ! : Convert current pane to window

C^x x : Ask to kill current pane
```



### Various commands
```
C^x d : Dettach current session
C^x r : Reload tmux.conf
C^x s : Menu to switch session
C^x P : Save history to file 
C^x t : Display clock
C^x ( : Move to previous session
C^x ) : Move to next session
C^x ? : Display shortcuts
```

### Panes resize
```
C^x : resize-pane -D (Resizes the current pane down)
C^x : resize-pane -U (Resizes the current pane upward)
C^x : resize-pane -L (Resizes the current pane left)
C^x : resize-pane -R (Resizes the current pane right)
C^x : resize-pane -D 20 (Resizes the current pane down by 20 cells)
C^x : resize-pane -U 20 (Resizes the current pane upward by 20 cells)
C^x : resize-pane -L 20 (Resizes the current pane left by 20 cells)
C^x : resize-pane -R 20 (Resizes the current pane right by 20 cells)
C^x : resize-pane -t 2 20 (Resizes the pane with the id of 2 down by 20 cells)
C^x : resize-pane -t -L 20 (Resizes the pane with the id of 2 left by 20 cells)

C^x C^up   : Resize pane +1 row to up (or down, right, left)
C^x Alt^up : Resize pane +5 row to up (or down, right, left)
```
  
### Panes sync
```
C^x :setw synchronize-panes : Enable/disable sync command to all panes
```
  
### Windows switch
```
C^x :swap-window -s 8 -t 5  : Switch the position of windows 8 and 5
C^x :swap-window -t 5       : Switch current window to window 5
C^x :swap-window -t +1      : Move current window to right (-1 to left)
C^x :move-window -t 2       : Move current window to window 2 and rename window number
```

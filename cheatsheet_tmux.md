# tmux 

.tmux.conf : https://github.com/alasta/config/blob/master/.tmux.conf

### Start New Session
```
tmux new -s SessionName
```

### Attach Session
Attach to last session
```
tmux attach
```
  
### Attach to Session Name  
```
tmux a -t SessionName
```

### Kill Session Name
```
tmux kill-session -t mysession
```

### Kill all sesion
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
F1  : Select window 1  
F2  : Select window 2  
F3  : Select window 3  
F4  : Select window 4  
F5  : Rename window name  
F6  : Split vertical window  
F7  : Split horizontal window   
F9  : Open new window  
F11 : Close current window  
F12 : Close all window
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

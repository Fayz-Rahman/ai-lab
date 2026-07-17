```python
import sys
import matplotlib

if sys.platform.startswith('linux'):
    matplotlib.use('Qt5Agg')

import matplotlib.pyplot as plt
import numpy as np
from matplotlib.colors import ListedColormap

# 2 room setup
length = 2
agent_loc = 0
hallway = [1, 1] 

plt.ion() 
fig, ax = plt.subplots(figsize=(4, 2)) 

room_cmap = ListedColormap(['green', 'saddlebrown', 'black'])

def draw_environment(hallway_state, current_agent_loc):
    ax.clear()
    
    grid_2d = np.array([hallway_state])
    ax.imshow(grid_2d, cmap=room_cmap, vmin=0, vmax=2)
    
    ax.plot(current_agent_loc, 0, marker='o', color='gold', markersize=40, markeredgecolor='black', markeredgewidth=2)
    
    ax.set_xticks(np.arange(-0.5, length, 1), minor=True)
    ax.set_yticks(np.arange(-0.5, 1, 1), minor=True)
    ax.grid(which='minor', color='black', linestyle='-', linewidth=3)
    ax.tick_params(which='minor', size=0) 
    
    ax.set_xticks([])
    ax.set_yticks([])
    
    plt.draw()
    plt.pause(1.0) 

# simulation loop 
draw_environment(hallway, agent_loc) 

while agent_loc < length - 1:   # 0 = 1st position
    
    if hallway[agent_loc] == 1:
        print(f"Cleaning room {agent_loc}")
        hallway[agent_loc] = 0
        draw_environment(hallway, agent_loc) 
    
    agent_loc += 1
    print(f"Moving right to room {agent_loc}")
    draw_environment(hallway, agent_loc) 

if hallway[agent_loc] == 1:
    print(f"Cleaning room {agent_loc}")
    hallway[agent_loc] = 0
    draw_environment(hallway, agent_loc)

plt.ioff()
plt.show()
```


### changes for 3rd task:
```python
length = 5  
agent_loc = 0
hallway = [1, 0, 2, 0, 1] 

plt.ion() 
fig, ax = plt.subplots(figsize=(8, 2)) 
```

```python
while agent_loc < length - 1 and hallway[agent_loc + 1] != 2:
```

### start at random

```python
import sys
import random
import matplotlib
import matplotlib.pyplot as plt
import numpy as np
from matplotlib.colors import ListedColormap

if sys.platform.startswith('linux'):
    matplotlib.use('Qt5Agg')

grid_size = 4
room = [[1 for _ in range(grid_size)] for _ in range(grid_size)]

agent_row = random.randint(0, grid_size - 1)
agent_col = random.randint(0, grid_size - 1)

plt.ion()
fig, ax = plt.subplots(figsize=(5, 5)) 
room_cmap = ListedColormap(['green', 'saddlebrown'])

def draw_2d_environment(room_state, current_row, current_col):
    """Draws a 2D matrix and overlays the agent using X, Y coordinates."""
    ax.clear()
    
    grid_2d = np.array(room_state)
    ax.imshow(grid_2d, cmap=room_cmap, vmin=0, vmax=1)
    
    ax.plot(current_col, current_row, marker='o', color='gold', markersize=35, markeredgecolor='black', markeredgewidth=2)
    
    ax.set_xticks(np.arange(-0.5, grid_size, 1), minor=True)
    ax.set_yticks(np.arange(-0.5, grid_size, 1), minor=True)
    ax.grid(which='minor', color='black', linestyle='-', linewidth=2)
    ax.tick_params(which='minor', size=0)
    
    ax.set_xticks([])
    ax.set_yticks([])
    
    plt.draw()
    plt.pause(0.5) 

print(f"Agent dropped at random location: ({agent_row}, {agent_col})")
draw_2d_environment(room, agent_row, agent_col)

while agent_row > 0 or agent_col > 0:
    
    if room[agent_row][agent_col] == 1:
        print(f"Cleaning ({agent_row}, {agent_col})")
        room[agent_row][agent_col] = 0
        draw_2d_environment(room, agent_row, agent_col)
        
    if agent_col > 0:
        agent_col -= 1
        print(f"Moving left to ({agent_row}, {agent_col})")
    elif agent_row > 0:
        agent_row -= 1
        print(f"Moving up to ({agent_row}, {agent_col})")
        
    draw_2d_environment(room, agent_row, agent_col)

print("Reached (0, 0). Beginning full sweep.")

for row in range(grid_size):
    agent_row = row
    
    if row % 2 == 0:
        cols_to_visit = range(0, grid_size)
    else:
        cols_to_visit = range(grid_size - 1, -1, -1)
        
    for col in cols_to_visit:
        agent_col = col
        
        if room[agent_row][agent_col] == 1:
            print(f"Cleaning ({agent_row}, {agent_col})")
            room[agent_row][agent_col] = 0
            
        print(f"Agent moved to ({agent_row}, {agent_col})")
        draw_2d_environment(room, agent_row, agent_col)

plt.ioff()
plt.show()
```

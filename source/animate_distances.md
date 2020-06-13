---
title: animate_distances
date: 2020-05-07
---
Example Python program animate_distances.py

## Modules

* import numpy as np
* import matplotlib
* from matplotlib import pyplot as plt
* from matplotlib import animation
* from .data import WALLS, TRAJECTORIES

## Methods

* def initialize_animation():
* def animate(i):

## Code

Python example

    import numpy as np
    import matplotlib
    matplotlib.use('TKAgg')
    from matplotlib import pyplot as plt
    from matplotlib import animation
    
    from .data import WALLS, TRAJECTORIES
    
    
    # First set up the figure, the axis, and the plot element we want to animate
    figure = plt.figure(figsize=(18, 6))
    axis = plt.axes(xlim=(-4.2, 4.2), ylim=(-4.2, 4.2))
    axis.set_aspect('equal', 'box')
    
    trajectory_lines = [
        axis.plot([], [], lw=2, marker='o', markersize=5)[0]
        for trajectory in TRAJECTORIES
    ]
    
    # line = axis.plot([], [], lw=2)[0]
    
    wall_lines = [
        axis.plot(*zip(*wall), lw=8, color='black')[0]
        for wall in WALLS
    ]
    
    
    # initialization function: plot the background of each frame
    def initialize_animation():
        return (*trajectory_lines, *wall_lines)
    
    
    # animation function.  This is called sequentially
    def animate(i):
        step_budget = i
    
        for j, (trajectory, trajectory_line) in enumerate(zip(
                TRAJECTORIES, trajectory_lines)):
            visible_data = trajectory[:min(step_budget, len(trajectory))]
            x, y = (zip(*visible_data)
                    if visible_data
                    else ((), ()))
            trajectory_line.set_data(x, y)
            step_budget -= len(visible_data)
    
        return (*trajectory_lines, *wall_lines)
    
    # call the animator.  blit=True means only re-draw the parts that have changed.
    anim = animation.FuncAnimation(
        figure,
        animate,
        init_func=initialize_animation,
        frames=sum(map(len, TRAJECTORIES)) + 6,
        interval=1000,
        blit=False)
    
    plt.axis('off')
    figure.tight_layout()
    # anim.save('basic_animation.mp4', fps=30, extra_args=['-vcodec', 'libx264'])
    anim.save('animation.gif', fps=10, writer='imagemagick')
    
    # plt.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

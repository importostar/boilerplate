---
title: choose_goal
date: 2020-05-07
---
Example Python program choose_goal.py

## Modules

* import numpy as np
* import matplotlib
* from matplotlib import pyplot as plt
* from matplotlib import animation
* from .data import WALLS, TRAJECTORIES

## Code

Python example

    import numpy as np
    import matplotlib
    matplotlib.use('TKAgg')
    from matplotlib import pyplot as plt
    from matplotlib import animation
    
    from .data import WALLS, TRAJECTORIES
    
    
    # First set up the figure, the axis, and the plot element we want to animate
    # figure = plt.figure()
    figure, axes = plt.subplots(1, 2)
    for axis in axes:
        axis.set_aspect('equal', 'box')
        axis.set_axis_off()
        axis.set_xlim((-4.2, 4.2))
        axis.set_ylim((-4.2, 4.2))
    
    trajectory_lines = [
        axes[0].plot(*zip(*trajectory), lw=2, marker='o', markersize=5)[0]
        for trajectory in TRAJECTORIES
    ]
    
    # line = axis.plot([], [], lw=2)[0]
    
    wall_lines = [
        axis.plot(*zip(*wall), lw=8, color='black')[0]
        for axis in axes
        for wall in WALLS
    ]
    
    axes[1].plot(*TRAJECTORIES[0][-1], marker='*', markersize=25)
    
    figure.tight_layout()
    # anim.save('basic_animation.mp4', fps=30, extra_args=['-vcodec', 'libx264'])
    # anim.save('animation.gif', fps=10, writer='imagemagick')
    
    plt.savefig('choose_goal.pdf')
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

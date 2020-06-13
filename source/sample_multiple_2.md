---
title: sample_multiple_2
date: 2020-05-07
---
Example Python program sample_multiple_2.py

## Modules

* import numpy as np
* from figure import Figure

## Code

Python example

    import numpy as np
    from figure import Figure
    
    x = np.linspace(0, 2 * np.pi, 1001)
    
    fig = Figure()
    fig.set_figsize((7, 7))
    fig.create_grid((3, 3))
    
    fig[:2, :2].create_grid((3, 3))
    for _i in range(3):
        for _j in range(3):
            fig[:2, :2][_i, _j].plot(
                np.cos(x) ** (_i * 2 + 1),
                np.sin(x) ** (_j * 2 + 1))
            fig[:2, :2][_i, _j].set_aspect("equal", "datalim")
    
    fig[:2, 2].plot(np.sin(x**2), x)
    fig[:2, 2].set_aspect("equal", "datalim")
    
    fig[2, :2].plot(x - np.sin(x), 1 - np.cos(x))
    fig[2, :2].set_aspect("equal", "datalim")
    
    y = 3 * x
    fig[2, 2].plot(np.cos(y) + y * np.sin(y), np.sin(y) - y * np.cos(y))
    fig[2, 2].set_aspect("equal", "datalim")
    
    fig.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

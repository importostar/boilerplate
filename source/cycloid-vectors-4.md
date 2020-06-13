---
title: cycloid vectors 4
date: 2020-05-07
---
Example Python program cycloid-vectors-4.py

## Modules

* import numpy as np
* from pathlib import Path
* import matplotlib.pyplot as plt
* from matplotlib import animation

## Methods

* def circle(a, b, r):

## Code

Python example

    import numpy as np
    from pathlib import Path
    import matplotlib.pyplot as plt
    from matplotlib import animation
    
    file_name = Path(__file__).resolve().stem
    
    
    def circle(a, b, r):
        resolution = 100
        x, y = [0] * resolution, [0] * resolution
        for i, theta in enumerate(np.linspace(0, 2 * np.pi, resolution)):
            x[i] = a + r * np.cos(theta)
            y[i] = b + r * np.sin(theta)
        return x, y
    
    
    thetas = np.linspace(0, 4 * np.pi, 128)
    cycloid_x = thetas - np.sin(thetas)
    cycloid_y = 1 - np.cos(thetas)
    cycloid_c = thetas
    
    fig = plt.figure()
    fig.dpi = 150
    fig.set_size_inches(4, 2)
    
    artists = []
    
    for i in range(len(thetas)):
        x, y = circle(cycloid_c[i], 1, 1)
        (rolling_circle,) = plt.plot(x, y, "g-", lw=2, alpha=0.4)
        (circle_center,) = plt.plot(cycloid_c[i], [1], "go", markersize=2, alpha=0.5)
        (cycloid_path,) = plt.plot(
            cycloid_x[: i + 1], cycloid_y[: i + 1], "r-", lw=1, alpha=0.5
        )
        (dot_on_circle,) = plt.plot(cycloid_x[i], cycloid_y[i], "ro", markersize=4)
        vectors = plt.quiver(
            [0, cycloid_c[i]],
            [0, 1],
            [cycloid_c[i], cycloid_x[i] - cycloid_c[i]],
            [1, cycloid_y[i] - 1],
            angles="xy",
            scale_units="xy",
            color=["b", "brown"],
            scale=1,
            lw=1,
            alpha=0.6,
        )
        artists.append(
            [rolling_circle, circle_center, cycloid_path, dot_on_circle, vectors]
        )
    
    plt.xlim(0, 4 * np.pi)
    plt.ylim(0, 3)
    plt.xticks(
        [0, np.pi, 2 * np.pi, 3 * np.pi, 4 * np.pi],
        [0, r"$\pi$", r"2 $\pi$", r"3 $\pi$", r"4 $\pi$"],
    )
    plt.yticks([0, 1, 2])
    plt.axes().set_aspect("equal")
    
    ani = animation.ArtistAnimation(fig, artists, interval=50, repeat_delay=0, blit=True)
    
    ani.save(file_name + ".mp4", writer="ffmpeg")
    ani.save(file_name + ".gif", writer="imagemagick")
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

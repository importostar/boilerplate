---
title: game_of_life (1)
date: 2020-05-07
---
Example Python program game_of_life (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import numpy as np
* from scipy.ndimage import convolve
* import matplotlib.pyplot as plt
* import matplotlib
* import copy

## Code

Python example

    import numpy as np
    from scipy.ndimage import convolve
    import matplotlib.pyplot as plt
    import matplotlib
    import copy
    
    # Setup
    BOARD_WIDTH = 10
    BOARD_HEIGHT = 10
    BOARD = np.zeros((BOARD_HEIGHT, BOARD_WIDTH))
    
    # Randomly initialize board
    MIN_ALIVE_START = 25
    MAX_ALIVE_START = 50
    num_alive_start = np.random.randint(MIN_ALIVE_START, MAX_ALIVE_START+1)
    print("Initializing {} alive squares".format(num_alive_start))
    kernel = np.array([[1, 1, 1],
                       [1, 0, 1],
                       [1, 1, 1]])
    
    # Assign alive cells to board
    for ii in range(num_alive_start):
        pos_x = np.random.randint(0, BOARD_WIDTH)
        pos_y = np.random.randint(0, BOARD_HEIGHT)
        BOARD[pos_y, pos_x] = 1
    
    print("This is the initial board. Please close to see next generation.")
    print("\n")
    
    plt.imshow(BOARD)
    matplotlib.pyplot.show()
    
    while True:
    
        old_board = copy.copy(BOARD)
    
        # Add up the neighbours on the board
        convolved_board = convolve(BOARD, kernel, mode="constant", cval=0.0)
    
        # Rule 1: die if less than 2
        BOARD[convolved_board < 2] = 0
    
        # Rule 2: die if more than 3
        BOARD[convolved_board > 3] = 0
    
        # Rule 3: alive if 3
        BOARD[convolved_board == 3] = 1
    
        plt.imshow(BOARD)
        matplotlib.pyplot.show()
    
        # If board hasn't changed or everything is dead, exit
        if np.all(BOARD == 0) or np.all(old_board == BOARD):
            break

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

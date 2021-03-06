---
title: show_rgb_channel
date: 2020-05-07
---
Example Python program show_rgb_channel.py


## Code

Python example

    # Note: we use the np.copy() function rather than just saying red_channel = image
    # because in Python, such a statement would set those two arrays equal to each other
    # forever, meaning any changes made to one would also be made to the other!
    red_channel = np.copy(image)
    # Note: here instead of extracting individual channels from the image
    # I'll keep all 3 color channels in each case but set the ones I'm not interested 
    # in to zero.  
    red_channel[:,:,[1, 2]] = 0 # Zero out the green and blue channels
    green_channel = np.copy(image)
    green_channel[:,:,[0, 2]] = 0 # Zero out the red and blue channels
    blue_channel = np.copy(image)
    blue_channel[:,:,[0, 1]] = 0 # Zero out the red and green channels
    fig = plt.figure(figsize=(12,3)) # Create a figure for plotting
    plt.subplot(131) # Initialize subplot number 1 in a figure that is 3 columns 1 row
    plt.imshow(red_channel) # Plot the red channel
    plt.subplot(132) # Initialize subplot number 2 in a figure that is 3 columns 1 row
    plt.imshow(green_channel)  # Plot the green channel
    plt.subplot(133) # Initialize subplot number 3 in a figure that is 3 columns 1 row
    plt.imshow(blue_channel)  # Plot the blue channel
    plt.show() 

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

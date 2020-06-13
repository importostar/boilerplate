---
title: queen
date: 2020-05-07
---
Example Python program queen.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Code

Python example

    n = int(input("Enter the dimension: "))
    init_x = int(input("Enter initial x pos: "))
    init_y = int(input("Enter initial y pos: "))
    final_x = int(input("Enter final x pos: "))
    final_y = int(input("Enter final y pos: "))
    
    where = final_y*final_x
    size = n*n
    
    if where > size:
        print("Please enter a valid index value.")
    else:
        while True:
            rem_x = (final_x - init_x) % 2
            rem_y = (final_y - init_y) % 2
    
            if init_y == final_y and init_x == final_x:
                print("catch")
                break
    
            elif final_x > init_x and rem_x == 0:
                # LowerLeft or LowerRight
                if final_y > init_y:
                    # add 2 to init_x and and 1 to init_y
                    init_x = init_x + 2
                    init_y = init_y + 1
                    print("New position1: ", "(", init_x, ",", init_y, ")")
    
                elif final_y < init_y:
                    # add 2 to init_x and subtract 1 from init_y
                    init_y = init_y - 1
                    init_x = init_x + 2
                    print("New position2: ", "(", init_x, ",", init_y, ")")
                else:
                    print("Invalid move!")
                    break
    
            elif final_x < init_x and rem_x == 0:
                # UpperLeft or UpperRight
                if final_y > init_y:
                    # subtract 2 from init_x and add 1 to init_y
                    init_x = init_x - 2
                    init_y = init_y + 1
                    print("New position3: ", "(", init_x, ",", init_y, ")")
    
                elif final_y < init_y:
                    # subtract 2 from init_x and subtract 1 from 1
                    init_y = init_y - 1
                    init_x = init_x - 2
                    print("New position4: ", "(", init_x, ",", init_y, ")")
                else:
                    print("Invalid move!!")
                    break
    
            elif final_x == init_x:
                # no movement in x axis
                if final_y > init_y and rem_y == 0:
                    # add 0 to init_x and add 2 to init_y
                    init_y = init_y + 2
                    print("New position5: ", "(", init_x, ",", init_y, ")")
    
                elif final_y < init_y and rem_y == 0:
                    # add 0 to init_x and subtract 2 from init_y
                    init_y = init_y - 2
                    print("New position6: ", "(", init_x, ",", init_y, ")")
                else:
                    print("Invalid move!!!")
                    break
    
            else:
                print("Invalid move!!!!")
                break
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: file
date: 2020-05-07
---
Example Python program file.py


## Code

Python example

    Difference between| r   r+   w   w+   a   a+
    ------------------|--------------------------
    read              | +   +        +        +
    write             |     +    +   +    +   +
    write after seek  |     +    +   +
    create            |          +   +    +   +
    truncate          |          +   +
    position at start | +   +    +   +
    position at end   |                   +   +
    where meanings are: (just to avoid any misinterpretation)
    
    read - reading from file is allowed
    write - writing to file is allowed
    create - file is created if it does not exist yet
    trunctate - during opening of the file it is made empty (all content of the file is erased)
    position at start - after file is opened, initial position is set to the start of the file
    position at end - after file is opened, initial position is set to the end of the file
    
    Note: a and a+ always append to the end of file - ignores any seek movements.
    BTW. interesting behavior at least on my win7 / python2.7, for new file opened in a+ mode:
    write('aa'); seek(0, 0); read(1); write('b') - second write is ignored
    write('aa'); seek(0, 0); read(2); write('b') - second write raises IOError

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

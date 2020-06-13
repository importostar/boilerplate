---
title: marlowe_procedural
date: 2020-05-07
---
Example Python program marlowe_procedural.py

## Modules

* import random
* import tkinter

## Code

Python tkinter example

    import random
    import tkinter
    
    text = []
    stat = [random.randrange(1,7) for i in range(4)]
    stat.remove(min(stat))
    text +=  ["+".join([str(roll) for roll in stat])] 
    text.append("=".join(str(sum(stat))))
    # now we do this another five times...
    stat = [random.randrange(1,7) for i in range(4)]
    stat.remove(min(stat))
    text +=  ["+".join([str(roll) for roll in stat])] 
    text.append("=".join(str(sum(stat))))
    stat = [random.randrange(1,7) for i in range(4)]
    stat.remove(min(stat))
    text +=  ["+".join([str(roll) for roll in stat])] 
    text.append("=".join(str(sum(stat))))
    stat = [random.randrange(1,7) for i in range(4)]
    stat.remove(min(stat))
    text +=  ["+".join([str(roll) for roll in stat])] 
    text.append("=".join(str(sum(stat))))
    stat = [random.randrange(1,7) for i in range(4)]
    stat.remove(min(stat))
    text +=  ["+".join([str(roll) for roll in stat])] 
    text.append("=".join(str(sum(stat))))
    stat = [random.randrange(1,7) for i in range(4)]
    stat.remove(min(stat))
    text +=  ["+".join([str(roll) for roll in stat])] 
    text.append("=".join(str(sum(stat))))
    
    root = tkinter.Tk()
    T = tkinter.Text(root, height=2, width=30)
    T.pack()
    T.insert("end", str(text))
    tkinter.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

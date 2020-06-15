---
title: classify_snow
date: 2020-05-07
---
Example Python program classify_snow.py

## Modules

* import os
* import tkinter
* import pandas as pd
* from PIL import Image
* from PIL import ImageTk

## Methods

* def button_click_exit_mainloop(event):
* def main():

## Code

Python tkinter example

    #!/usr/bin/env python
    """
    Script to loop through images and categorize them in some way.
    """
    
    import os
    import tkinter
    import pandas as pd
    from PIL import Image
    from PIL import ImageTk
    
    # Maximum dimensions of image
    MAX_WIDTH = 800
    MAX_HEIGHT = 600
    
    # Where to get the images from
    DIRNAME = './Original_Images'
    
    # Store the data
    EVENTS = []
    DATES = []
    
    # Map the data
    MAP = {1: 'open',
           2: 'light snow',
           3: 'heavy snow'}
    
    
    def button_click_exit_mainloop(event):
        EVENTS.append(int(event.char))
        event.widget.quit()
    
    
    def main():
        root = tkinter.Tk()
        root.bind("<Key>", button_click_exit_mainloop)
        root.geometry('+{}+{}'.format(100, 100))
        dirlist = os.listdir(DIRNAME)
        old_label_image = None
        for f in dirlist:
            try:
                image = Image.open('{}/{}'.format(DIRNAME, f))
                img_date = image._getexif()[36867]
                DATES.append(img_date)
                width = min([MAX_WIDTH, image.size[0]])
                height = min([MAX_HEIGHT, image.size[1]])
                image = image.resize((width, height), Image.ANTIALIAS)
                root.geometry('{}x{}'.format(width, height))
                tkpi = ImageTk.PhotoImage(image)
                label_image = tkinter.Label(root, image=tkpi)
                label_image.place(x=0, y=0, width=width, height=height)
                root.title(f)
                if old_label_image is not None:
                    old_label_image.destroy()
                old_label_image = label_image
                root.mainloop()
            except:
                # Skip things that aren't images
                pass
        # Write out the data
        df = pd.DataFrame({'raw': EVENTS,
                           'snow_level': [MAP[i] for i in EVENTS],
                           'date': DATES})
        df.to_csv('./processed.csv')
        # Make sure that we kill the interface when we're done
        root.destroy()
    
    
    if __name__ == '__main__':
        main()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

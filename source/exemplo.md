---
title: exemplo
date: 2020-05-07
---
Example Python program exemplo.py

## Modules

* import tkinter as tk
* from PIL import Image, ImageDraw, ImageTk

## Code

Python tkinter example

    import tkinter as tk
    from PIL import Image, ImageDraw, ImageTk
    
    im = Image.new('RGB', (256, 256))
    draw = ImageDraw.Draw(im)
    
    width = 256
    height = 256
    
    cor1 = (255, 0, 0)
    cor2 = (0, 0, 255)
    
    even = True
    
    inicio = 0
    tamanho = 16
    
    for x1 in range(inicio, height, tamanho):
        even = not even
        for y1 in range(inicio, width, tamanho):
            x2 = x1+tamanho
            y2 = y1+tamanho
            coord = (x1, y1, x2, y2)
            even = not even
            if even:
                draw.rectangle(coord, fill=cor1)
            else:
                draw.rectangle(coord, fill=cor2)
    
    im.save("chessboard.png")
    
    # Initializing tkinter
    root = tk.Tk()
    root.title('Shot Viewer')
    w, h, x, y = 256, 256, 0, 0
    root.geometry("%dx%d+%d+%d" % (w, h, x, y))
    
    # Loading Image on tkinter
    photo = tk.PhotoImage(file="chessboard.png")
    photo_label = tk.Label(image=photo)
    photo_label.grid()
    photo_label.image = photo
    
    root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

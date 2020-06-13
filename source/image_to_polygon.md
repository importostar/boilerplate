---
title: image_to_polygon
date: 2020-05-07
---
Example Python program image_to_polygon.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import numpy as np
* import matplotlib.pyplot as plt
* import matplotlib.image as mpimg
* from matplotlib.patches import Polygon
* from matplotlib.collections import PatchCollection

## Code

Python example

    """
    To install the matplotlib module :
    https://matplotlib.org/users/installing.html
    """
    
    import numpy as np
    import matplotlib.pyplot as plt
    import matplotlib.image as mpimg
    from matplotlib.patches import Polygon
    from matplotlib.collections import PatchCollection
    
    '''
    Method only .png image files are supported
    ===> To manage photos, It can be easily done online at: " www.iloveimg.com "
    '''
    # path image file
    img_file = "C:/Users/Teerapong/Desktop/myturtle.png"
    
    # set to polygon size
    polygons_size = 6
    
    # mapping image file to array bit color
    img = mpimg.imread(img_file)
    
    # check bit color of image file
    '''
    bit color ===> have 3 value = 24-bit color
    can not be translucent.
    so it creates polygon is full image
    '''
    is_img_24_bit = len(img[0][0]) == 3
    
    img_width = len(img[0])         # number column
    img_height = len(img)           # number row
    
    # display
    print("Image file name: ",img_file)
    print('Image size: ', img_width, 'x', img_height)
    print('Polygon size: ', polygons_size)
    print("Image is 24-bit color: ", is_img_24_bit)
    print('---Processing---')
    
    patches = []    # initial # keep point for build polygon
    colors = []     # initial # keep color for each polygon
    count_all = 0   # count all around
    
    """ 
    Example (32-bit color)
    ===> array color = [1., 1., 1., 0.]
    ===> is pixel none color, blank blackground
    ===> final index in array color is transparent
    ===> transparent=1=TRUE / transparent=0=FALSE
    """
    
    # create polygon
    half_poly_size = polygons_size / 2.
    
    '''
    x and y that control while-loop
                                         x1   x2
                                         |    |
                                         V    V
              /\------/          |       /\------/  
             /  \    /           |      /  \    /  
            /    \  /            |     /    \  /   
     y1--> /______\/             |    /______\/   
           \      /\             |    \      /\   
            \    /  \            |     \    /  \ 
             \  /    \           |      \  /    \
     y2-->    \/______\          |       \/______\
     
     y2 = y1+polygons_size              x2 = x1+half_poly_size
     
    '''
    y = polygons_size
    while y <= img_height:
        x = half_poly_size      # set initial value of x
        while x <= (img_width-half_poly_size):
            # next count_all
            count_all += 1
    
            '''
            ---get pixel color ---
                /\--------/
               /  \   X  /
              /    \    /
             /   X  \  /
            /________\/
            
            (X) point is to get pixel color, Where is center of triangle
            
            '''
            pix_color = img[int(y - half_poly_size)][int(x)]
    
            # 32-color bit case:
            # in pix_color list, final index is transparent
            #
            # transparent = pix_color[-1]
            # transparent = pix_color[len(pix_color)-1]
    
            if is_img_24_bit or pix_color[-1] != 0:
                '''
                --- Method forms of creation Polygon ---
                # check y mod (polygons_size*2) == 0
                #   ===> similar to check odd-event number
                #   ===> to switch forms of creation Polygon
                # check x mod polygons_size == 0
                #   ===> same with y check
                
                if y % (polygons_size*2) == 0:
                    x % polygons_size == 0
                        points = np.array([[x, y], [x-half, y-polygons_size], [x+half, y-polygons_size]])
                    else:
                        points = np.array([[x-half, y], [x, y-polygons_size], [x+half, y]])
                else:
                    if x % polygons_size == 0
                        points = np.array([[x-half, y], [x, y-polygons_size], [x+half, y]])
                    else:
                        points = np.array([[x, y], [x-half, y-polygons_size], [x+half, y-polygons_size]])
                '''
    
                # --- Method forms of creation Polygon ---
                # XOR logical
                if (y % (polygons_size*2) == 0) ^ (x % polygons_size == 0):
                    points = np.array([[x, y], [x-half_poly_size, y-polygons_size], [x+half_poly_size, y-polygons_size]])
                else:
                    points = np.array([[x-half_poly_size, y], [x, y-polygons_size], [x+half_poly_size, y]])
    
                # build-in patches point to patches Polygon object and append to patches list
                patches.append(Polygon(points))
                # append pixel color to colors list
                colors.append(pix_color)
            # end if transparent
    
            x += half_poly_size     # next x
        # end while-loop: x
    
        y += polygons_size      # next y
    # end while-loop: y
    
    print('---complete(1)---')
    
    ''' 
    Documents for color map : https://matplotlib.org/users/colormaps.html 
    or color example code : https://matplotlib.org/xkcd/examples/color/colormaps_reference.html
    '''
    
    color_map = "Paired"    # similar to color tone
    color_intensity = 0.5   # value between 0 and 1
    
    # patch collection
    p = PatchCollection(patches, cmap=plt.get_cmap(color_map), alpha=color_intensity)
    print('---complete(2)---')
    
    p.set_color(colors)     # set color by color list
    print('---complete(3)---')
    
    # set figure and axes
    fig = plt.figure()
    ax = plt.Axes(fig, [0., 0., 1., 1.])
    fig.add_axes(ax)
    ax.add_collection(p)
    
    ''' setting save and show image '''
    plt.xlim(0, img_width)
    plt.ylim(img_height, 0)
    
    # set size of image to save
    # similar with resize image file
    
    # save_img_size = int(600)   # 600*600 pixel
    # fig.set_size_inches(save_img_size/100., save_img_size/100.)   # inches = pixel/100.0
    
    fig.set_size_inches(img_width/100., img_height/100.)   # inches = pixel/100.0
    
    # save image
    file_save = 'polygon_'+img_file.split("/")[-1]
    plt.savefig(file_save)
    
    # display
    print('Polygon all possible in image: ', count_all)
    print('Polygon used to build: ', len(colors))      # same with ===> len(patches)), count number of build polygon
    print('---Save file---')
    print('Image size: %dx%d' % (save_img_size, save_img_size))
    print('File name: ', file_save)
    
    plt.show()  # show image
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

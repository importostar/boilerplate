---
title: functions (1)
date: 2020-05-07
---
Example Python program functions (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os
* import numpy as np
* import pandas as pd
* from tqdm import tqdm
* import keras.backend as K
* import cv2
* import matplotlib.pyplot as plt
* from matplotlib.backends.backend_agg import FigureCanvasAgg as FigureCanvas
* from matplotlib.figure import Figure

## Methods

* def get_activations(model, model_inputs, print_shape_only=False, layer_name=None):
* def display_activations(activation_maps, cmap='inferno'):
* def norm_pixels(img):
* def get_figure(img, img_size=(250,70), dpi=70., cmap='inferno'):
* def crop(img, xmin=700,xmax=4300,vmin=2500,vmax=16000):

## Code

Python example

    # Default Python's libraries
    import os
    
    
    import numpy as np
    import pandas as pd
    from tqdm import tqdm
    import keras.backend as K
    
    # Graphic libraries
    import cv2
    import matplotlib.pyplot as plt
    from matplotlib.backends.backend_agg import FigureCanvasAgg as FigureCanvas
    from matplotlib.figure import Figure
    
    
    def get_activations(model, model_inputs, print_shape_only=False, layer_name=None):
        '''Get model activation map at any layer.
    
        model: Keras ConvNet model
        model_inputs: Input image to be evaluated: Shape (1, 70, 250)
        print_shape_only: Flag to only print activation map shape
        layer_name: name or list of layer names to plot.
        Returns: Desired activation maps
        '''
        activations = []
        inp = model.input
    
        model_multi_inputs_cond = True
        if not isinstance(inp, list):
            # only one input! let's wrap it in a list.
            inp = [inp]
            model_multi_inputs_cond = False
    
        # Modifications to accept a list of layer names
        outputs = []
        if layer_name == None:
            layer_name = [model.layers[i].name for i in range(len(model.layers))]
        
        if layer_name != None and type(layer_name) is str:
            layer_name =[layer_name]
        
        for layer in model.layers:
            for name in layer_name:
                if layer.name == name:
                    outputs.append(layer.output)
        
        funcs = [K.function(inp + [K.learning_phase()], [out]) for out in outputs]  # evaluation functions
    
        if model_multi_inputs_cond:
            list_inputs = []
            list_inputs.extend(model_inputs)
            list_inputs.append(0.)
        else:
            list_inputs = [model_inputs, 0.]
    
        # Learning phase. 0 = Test mode (no dropout or batch normalization)
        # layer_outputs = [func([model_inputs, 0.])[0] for func in funcs]
        layer_outputs = [func(list_inputs)[0] for func in funcs]
        
        for layer_activations in layer_outputs:
            activations.append(layer_activations)
    
        return activations
    
    
    def display_activations(activation_maps, cmap='inferno'):
        '''Display activations obtained from get_activations function.
    
        You can parse any matplotlib built in cmap.
        '''
        batch_size = activation_maps[0].shape[0]
        assert batch_size == 1, 'One image at a time to visualize.'
        for i, activation_map in enumerate(activation_maps):
          #  print('Displaying activation map {}'.format(i))
            shape = activation_map.shape
            if len(shape) == 4:
                activations = np.hstack(np.transpose(activation_map[0], (2, 0, 1)))
            elif len(shape) == 2:
                # try to make it square as much as possible. we can skip some activations.
                activations = activation_map[0]
                num_activations = len(activations)
                if num_activations > 1024:  # too hard to display it on the screen.
                    square_param = int(np.floor(np.sqrt(num_activations)))
                    activations = activations[0: square_param * square_param]
                    activations = np.reshape(activations, (square_param, square_param))
                else:
                    activations = np.expand_dims(activations, axis=0)
            else:
                raise Exception('len(shape) = 3 has not been implemented.')
            
            plt.imshow(activations, interpolation='None', cmap=cmap)
            
        return None        
    
    
    def norm_pixels(img):
        '''Normalise pixel values from the activation maps in range 0 -255'''
        pix = ((img) - img.min()) / ((img.max() - img.min()))
        return pix * 255
    
    
    def get_figure(img, img_size=(250,70), dpi=70., cmap='inferno'):
        '''Get numpy array figure from matplotlib canvas. 
    
        '''
        h_size, v_size = img_size
        xinch = h_size / dpi
        yinch = v_size  / dpi 
    
        fig = plt.figure(figsize=(xinch,yinch))
        width, height = fig.get_size_inches() * fig.get_dpi() 
    
        canvas = FigureCanvas(fig)
        ax = fig.gca()
        ax.imshow(img,cmap=cmap)
        ax.axis('off')
        plt.close()
    
        canvas.draw()       # draw the canvas, cache the renderer
        image = np.fromstring(canvas.tostring_rgb(), dtype='uint8')
        img = image.reshape(int(height), int(width), 3)
        
        return img
    
    
    def crop(img, xmin=700,xmax=4300,vmin=2500,vmax=16000):
        '''Remove matplotlib canvas from image.
    
        Returns: cropped image'''
        return img[xmin:xmax,vmin:vmax]
        
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

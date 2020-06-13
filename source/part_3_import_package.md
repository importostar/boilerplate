---
title: part_3_import_package
date: 2020-05-07
---
Example Python program part_3_import_package.py

## Modules

* import matplotlib
* # import the necessary packages
* from sklearn.preprocessing import LabelBinarizer
* from sklearn.model_selection import train_test_split
* from sklearn.metrics import classification_report
* from keras.preprocessing.image import ImageDataGenerator
* from keras.optimizers import SGD
* from keras.models import Sequential
* from keras.layers.normalization import BatchNormalization
* from keras.layers.convolutional import Conv2D
* from keras.layers.convolutional import MaxPooling2D
* from keras.layers.core import Activation
* from keras.layers.core import Flatten
* from keras.layers.core import Dropout
* from keras.layers.core import Dense
* from keras import backend as K
* from imutils import paths
* import matplotlib.pyplot as plt
* import numpy as np
* import argparse
* import random
* import pickle
* import cv2
* import os

## Code

Python example

    # set the matplotlib backend so figures can be saved in the background
    import matplotlib
    matplotlib.use("Agg")
    
    # import the necessary packages
    
    from sklearn.preprocessing import LabelBinarizer
    from sklearn.model_selection import train_test_split
    from sklearn.metrics import classification_report
    from keras.preprocessing.image import ImageDataGenerator
    from keras.optimizers import SGD
    from keras.models import Sequential
    from keras.layers.normalization import BatchNormalization
    from keras.layers.convolutional import Conv2D
    from keras.layers.convolutional import MaxPooling2D
    from keras.layers.core import Activation
    from keras.layers.core import Flatten
    from keras.layers.core import Dropout
    from keras.layers.core import Dense
    from keras import backend as K
    from imutils import paths
    import matplotlib.pyplot as plt
    import numpy as np
    import argparse
    import random
    import pickle
    import cv2
    import os

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

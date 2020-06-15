---
title: 9_21_cnn_model_2
date: 2020-05-07
---
Example Python program 9_21_cnn_model_2.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tensorflow as tf
* import matplotlib.pyplot as plt
* import numpy as np
* import os

## Methods

* def conv2d(_input, filters):
* def max_pooling2d(_input):

## Code

Python example

    import tensorflow as tf
    import matplotlib.pyplot as plt
    import numpy as np
    import os
    %matplotlib inline
    
    image_path = './Test_Dataset_png'
    image_file_paths = [os.path.join(image_path, filename) 
                  for filename in os.listdir(image_path)]
    
    label_path = ['./label_csv/Label.csv']
    
    tf.reset_default_graph()
    image_filename_queue = tf.train.string_input_producer(image_file_paths, shuffle=False)
    label_filename_queue = tf.train.string_input_producer(label_path, shuffle=False)
    
    image_reader = tf.WholeFileReader()
    label_reader = tf.TextLineReader()
    
    image_key, image_value = image_reader.read(image_filename_queue)
    label_key, label_value = label_reader.read(label_filename_queue)
    
    decoded_img = tf.image.decode_png(image_value)
    decoded_csv = tf.decode_csv(label_value, record_defaults=[[0]])
    
    decoded_img = tf.reshape(decoded_img, [61, 49, 1])
    
    batch_size = 20
    x, y_ = tf.train.batch(
        [decoded_img, decoded_csv], 
        batch_size=batch_size)
    
    x = tf.cast(x, tf.float32)
    y_ = tf.one_hot(y_, 3, axis=1, dtype=tf.float32)
    y_ = tf.reshape(y_, [-1, 3])
    print(y_.shape)
    
    
    
    def conv2d(_input, filters):
        return tf.layers.conv2d(_input,
                               filters=filters,
                                kernel_size=3,
                                activation=tf.nn.relu,
                                padding="SAME")
    
    def max_pooling2d(_input):
        return tf.layers.max_pooling2d(_input,
                                      pool_size=2,
                                      strides=[2, 2])
    
    conv1 = conv2d(x, 10)
    print(conv1.shape)
    pool1 = max_pooling2d(conv1)
    print(pool1.shape)
    conv2 = conv2d(pool1, 20)
    print(conv2.shape)
    pool2 = max_pooling2d(conv2)
    
    print(pool2.shape)
    row = int(pool2.shape[1])
    column = int(pool2.shape[2])
    depth = int(pool2.shape[3])
    flat = tf.reshape(pool2, [-1, row*column*depth])
    print(flat.shape)
    
    fc1 = tf.layers.dense(flat, 2000)
    fc2 = tf.layers.dense(fc1, 1000)
    out = tf.layers.dense(fc2, 3)
    
    print(y_.shape)
    print(out.shape)
    loss = tf.losses.softmax_cross_entropy(y_, out)
    print(loss.shape)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

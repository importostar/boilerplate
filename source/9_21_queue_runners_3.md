---
title: 9_21_queue_runners_3
date: 2020-05-07
---
Example Python program 9_21_queue_runners_3.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tensorflow as tf
* import matplotlib.pyplot as plt
* import numpy as np
* import os

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
    
    decoded_img = tf.reshape(decoded_img, [61, 49])
    
    batch_size = 20
    x, k, y_ = tf.train.batch(
        [decoded_img, image_key, decoded_csv], 
        batch_size=batch_size)
    
    with tf.Session() as sess:
        coord = tf.train.Coordinator()
        thread = tf.train.start_queue_runners(sess, coord)
        
        _img, _key = sess.run([x, k])
        for i in range(batch_size):
            plt.imshow(_img[i])
            print(_key[i])
            plt.figure(i+1)
     
        coord.request_stop()
        coord.join(thread)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

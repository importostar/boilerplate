---
title: 10_19_pipeline (1)
date: 2020-05-07
---
Example Python program 10_19_pipeline (1).py
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
    
    image_dir = "./image_png"
    image_names = os.listdir(image_dir)
    images = [os.path.join(image_dir, name) for name in image_names]
    
    imagename_queue = tf.train.string_input_producer(images, shuffle=False)
    labelname_queue = tf.train.string_input_producer(['./label_csv/Label.csv'], shuffle=False)
    
    
    image_reader = tf.WholeFileReader()
    key, raw_img = image_reader.read(imagename_queue)
    
    csv_reader = tf.TextLineReader()
    key, raw_txt = csv_reader.read(labelname_queue)
    
    png_image = tf.image.decode_png(raw_img)
    csv_label = tf.decode_csv(raw_txt, record_defaults=[[0]])
    
    png_image = tf.reduce_mean(png_image, axis=2)
    
    png_image = tf.reshape(png_image, [61, 49])
    
    x, y_ = tf.train.batch([png_image, csv_label], 32)
    
    
    with tf.Session() as sess:
        coord = tf.train.Coordinator()
        thread = tf.train.start_queue_runners(sess, coord)
        
        _image, _label = sess.run([x, y_])
        for i in range(32):
            plt.figure(i)
            print('age: {}'.format(_label[i]))
            plt.imshow(_image[i])
        
        coord.request_stop()
        coord.join(thread)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

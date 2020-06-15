---
title: 10_19_cnn_model (1)
date: 2020-05-07
---
Example Python program 10_19_cnn_model (1).py
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
    png_image = tf.reshape(png_image, [61, 49, 1])
    
    #x, y_ = tf.train.batch([png_image, csv_label], 32)
    x, y_ = tf.train.shuffle_batch([png_image, csv_label], batch_size=32, capacity=50000, min_after_dequeue=10000)
    x = tf.cast(x, tf.float32)
    
    y_ = tf.reshape(y_, [-1])
    y_ = tf.one_hot(y_,depth=3, on_value=1.0, off_value=0.0, axis=-1, dtype=tf.float32)
    #y_ = tf.reduce_mean(y_,axis=2)
    
    
    
    conv1 = tf.layers.conv2d(x, filters=13, kernel_size=[3,3], activation=tf.nn.relu, padding="SAME")
    conv2 = tf.layers.conv2d(conv1, filters=36, kernel_size=[3,3], activation=tf.nn.relu, padding="SAME")
    pool2 = tf.layers.max_pooling2d(conv2, pool_size=[2,2], strides=[2,2])
                                    
    conv3 = tf.layers.conv2d(pool2, filters=50, kernel_size=[3,3], activation=tf.nn.relu, padding="SAME")
    pool3 = tf.layers.max_pooling2d(conv3, pool_size=[2,2], strides=[2,2])
    
    conv4 = tf.layers.conv2d(pool3, filters=20, kernel_size=[3,3], activation=tf.nn.relu, padding="SAME")
    pool4 = tf.layers.max_pooling2d(conv4, pool_size=[2,2], strides=[2,2])
    
    fc_input_size = int(pool4.shape[1])*int(pool4.shape[2])*int(pool4.shape[3])
    flat = tf.reshape(pool4, shape=[-1, fc_input_size])
    
    drop_prob = tf.placeholder(tf.float32)
    
    fc1 = tf.layers.dense(flat, units=300)
    dropout1 = tf.layers.dropout(fc1, drop_prob)
    
    fc2 = tf.layers.dense(dropout1, units=100)
    dropout2 = tf.layers.dropout(fc2, drop_prob)
    
    out = tf.layers.dense(dropout2, units=3)
    
    loss = tf.losses.softmax_cross_entropy(y_, out)
    tf.summary.scalar("loss",loss)
    
    train_op = tf.train.GradientDescentOptimizer(1e-6).minimize(loss)
    
    merged = tf.summary.merge_all()
    
    with tf.Session() as sess:
        coord = tf.train.Coordinator()
        thread = tf.train.start_queue_runners(sess, coord)    
        writer = tf.summary.FileWriter('./logs/', sess.graph)
        sess.run(tf.global_variables_initializer())
        
        for i in range(100):    
            _, _loss, _summaries = sess.run([train_op, loss, merged], feed_dict={drop_prob:0.7})
            writer.add_summary(_summaries, i)
            if(i%10 == 0):
                print(_loss)
    
        
        coord.request_stop()
        coord.join(thread)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

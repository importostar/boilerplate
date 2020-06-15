---
title: logistic_regression_log_loss
date: 2020-05-07
---
Example Python program logistic_regression_log_loss.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tensorflow as tf
* import matplotlib.pyplot as plt
* import numpy as np

## Code

Python example

    import tensorflow as tf
    import matplotlib.pyplot as plt
    import numpy as np
    %matplotlib inline
    
    samples = 1000
    data = [1e-2*float(i) for i in range(-samples, samples)]
    label = [1 if i>3.14 else 0 for i in range(-samples, samples)]
    plt.scatter(data, label, 1, 'r')
    
    x = tf.placeholder(tf.float32)
    y_ = tf.placeholder(tf.float32)
    
    w = tf.Variable(0.0, dtype=tf.float32)
    b = tf.Variable(0.0, dtype=tf.float32)
    
    y = tf.nn.sigmoid(w*x + b)
    
    loss = tf.losses.log_loss(y_, y)
    train_op = tf.train.GradientDescentOptimizer(1e-2).minimize(loss)
    
    init = tf.global_variables_initializer()
    
    with tf.Session() as sess:
        sess.run(init)
        for i in range(10000):
            _, _loss = sess.run([train_op, loss], {x: data, y_: label})
            if i%100 == 0:
                _pred = sess.run(y, {x: data})
                plt.scatter(data, label, 1, 'b')
                plt.scatter(data, _pred, 1, 'r')
                print('step: {}, loss: {}'.format(i, _loss))

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

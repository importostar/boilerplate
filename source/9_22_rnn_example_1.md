---
title: 9_22_rnn_example_1
date: 2020-05-07
---
Example Python program 9_22_rnn_example_1.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tensorflow as tf
* import numpy as np
* import matplotlib.pyplot as plt

## Code

Python example

    import tensorflow as tf
    import numpy as np
    import matplotlib.pyplot as plt
    %matplotlib inline
    
    samples = 1000
    domain = np.array([float(i)*0.01 for i in range(samples + 1)], np.float32)
    sin = np.sin(domain)
    
    tf.reset_default_graph()
    
    time_step = 5
    features = 1
    state_size = 15
    
    x_reshaped = tf.reshape(sin[:-1], [-1, time_step, features])
    y_reshaped = tf.reshape(sin[1:], [-1, time_step, features])
    
    x = tf.unstack(x_reshaped, axis=1)
    y_ = tf.unstack(y_reshaped, axis=1)
    
    rnn_cell = tf.nn.rnn_cell.BasicRNNCell(num_units=state_size)
    output, state = tf.nn.static_rnn(cell=rnn_cell, inputs=x, dtype=tf.float32)
    
    kernel_init = tf.truncated_normal(shape=[time_step, state_size, features])
    bias_init = tf.zeros(features)
    
    output_w = tf.Variable(kernel_init)
    output_b = tf.Variable(bias_init)
    
    y = tf.matmul(output, output_w) + output_b
    
    print(y.shape)
    print(len(y_), y_[0].shape)
    
    
    for t in range(time_step):
        print(y[t].shape, y_[t].shape)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

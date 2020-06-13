---
title: rnn_signal_classification
date: 2020-05-07
---
Example Python program rnn_signal_classification.py
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
    
    tf.reset_default_graph()
    
    samples = 1000
    
    time_step = 5
    features = 1
    state_size = 15
    
    domain = np.array([float(i)*0.01 for i in range(samples)], np.float32)
    sinx = np.sin(domain)
    sin2x = np.sin(2*domain)
    plt.figure(0)
    plt.plot(sinx)
    plt.figure(1)
    plt.plot(sin2x)
    
    
    sinx_reshaped = np.reshape(sinx, [-1, time_step, features])
    sin2x_reshaped = np.reshape(sin2x, [-1, time_step, features])
    
    batch_size = int(sinx_reshaped.shape[0])
    
    train_data = []
    label_data = []
    for i in range(batch_size):
        train_data.append(sinx_reshaped[i])
        train_data.append(sin2x_reshaped[i])
        label_data.append([0.])
        label_data.append([1.])
    
    
    train_data = np.array(train_data, dtype=np.float32)
    label_data = np.array(label_data, dtype=np.float32)
    
    train_data = tf.constant(train_data, dtype=tf.float32)
    label_data = tf.constant(label_data, dtype=tf.float32)
    
    train_data = tf.unstack(train_data, axis=1)
    
    rnn_cell = tf.nn.rnn_cell.BasicRNNCell(num_units=state_size)
    output, state = tf.nn.static_rnn(cell=rnn_cell, inputs=train_data, dtype=tf.float32)
    
    kernel_init = tf.truncated_normal(shape=[time_step, state_size, features])
    bias_init = tf.zeros(features)
    
    output_w = tf.Variable(kernel_init)
    output_b = tf.Variable(bias_init)
    
    y = tf.matmul(output, output_w) + output_b
    
    pred = tf.nn.sigmoid(y[-1])
    
    loss = tf.losses.sigmoid_cross_entropy(label_data, y[-1])
    train_op = tf.train.GradientDescentOptimizer(1e-2).minimize(loss)
    
    with tf.Session() as sess:
        sess.run(tf.global_variables_initializer())
        for i in range(10000):
            _, _loss = sess.run([train_op, loss])
            
            if i%200 == 0:
                print('step: {} loss: {}'.format(i, _loss))
                
        _pred = sess.run(pred)
        print(_pred[:10])

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

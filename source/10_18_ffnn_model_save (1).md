---
title: 10_18_ffnn_model_save (1)
date: 2020-05-07
---
Example Python program 10_18_ffnn_model_save (1).py
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
    up = [i for i in range(10)]
    down = [9-i for i in range(10)]
    data = [up if i%2 == 0 else down for i in range(samples)]
    label = [[1] if i%2 == 0 else [0] for i in range(samples)]
    for d, l in zip(data[:10], label[:10]):
        print(d, l)
    
    tf.reset_default_graph()
    
    x = tf.placeholder(tf.float32, shape=[None, 10])
    y_ = tf.placeholder(tf.float32, shape=[None, 1])
    
    layer1 = tf.layers.dense(x, units=10, name='l1')
    layer2 = tf.layers.dense(layer1, units=5, name='l2')
    layer3 = tf.layers.dense(layer2, units=7, name='l3')
    out = tf.layers.dense(layer3, units=1, name='l4')
    
    variables = tf.trainable_variables()
    for v in variables:
        print(v)
    
    saver = tf.train.Saver(variables)
    
    loss = tf.losses.sigmoid_cross_entropy(y_, out)
    train_op = tf.train.GradientDescentOptimizer(1e-2).minimize(loss)
    
    pred = tf.nn.sigmoid(out)
    accuracy = tf.metrics.accuracy(y_, tf.round(pred))
    
    with tf.Session() as sess:
        sess.run(tf.global_variables_initializer())
        sess.run(tf.local_variables_initializer())
        for i in range(100):
            _, _loss = sess.run([train_op, loss], feed_dict={x: data, y_: label})
            if i%10 == 0:
                saver.save(sess, './logs/ffnn_model')
                _pred, _acc = sess.run([pred, accuracy], feed_dict={x: data, y_:label})
                print('loss: {}'.format(_loss))
                print('\nprediction')
                for d, p, a in zip(data[:10], _pred[:10], _acc[:10]):
                    print('{}{}{}'.format(d, p, a))

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: SAE
date: 2020-05-07
---
Example Python program SAE.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import tensorflow as tf
* import sys
* import os
* from evaluations import *
* from tensorflow.examples.tutorials.mnist import input_data
* import numpy as np
* from tensorflow import truncated_normal_initializer as normal_init
* #  from tensorflow.contrib.layers import variance_scaling_initializer as var_init

## Classes

* class decay_lr(tf.keras.callbacks.Callback):

## Methods

* def __init__(self, n_epoch, decay):
* def on_epoch_begin(self, epoch, logs={}):
* def load_mnist(val_size=0, path='/tmp/mnist/'):

## Code

Python example

    #! /usr/bin/env python
    
    import tensorflow as tf
    import sys
    import os
    from evaluations import *
    from tensorflow.examples.tutorials.mnist import input_data
    import numpy as np
    
    # Suppress tensorflow warnings
    
    os.environ['TF_CPP_MIN_LOG_LEVEL'] = '3'
    tf.logging.set_verbosity(tf.logging.ERROR)
    
    # Session settings to avoid pre allocating all the GPU memory
    
    config = tf.ConfigProto()
    config.gpu_options.allow_growth = True
    sess = tf.Session(config=config)
    tf.keras.backend.set_session(sess)
    
    # Create custom learning rate decay scheduler
    # We want to decay the learning rate on specific epoch numbers
    
    class decay_lr(tf.keras.callbacks.Callback):
        ''' 
            n_epoch = no. of epochs after decay should happen.
            decay = decay value
        '''  
        def __init__(self, n_epoch, decay):
            super(decay_lr, self).__init__()
            self.n_epoch=n_epoch
            self.decay=decay
    
        def on_epoch_begin(self, epoch, logs={}):
            old_lr = self.model.optimizer.lr
            old_lr = tf.keras.backend.get_value(old_lr)
            # If current epoch is divided by decay epoch then decay lr
            if epoch % self.n_epoch == 0 and epoch != 0:
                new_lr= self.decay*old_lr
                tf.keras.backend.set_value(self.model.optimizer.lr, new_lr)
            else:
                tf.keras.backend.set_value(self.model.optimizer.lr, old_lr)
    
    
    # Download / Extract mnist data
    
    def load_mnist(val_size=0, path='/tmp/mnist/'):
        mnist = input_data.read_data_sets(
            path, validation_size=val_size)
        return mnist
    
    
    ##############################################################################
    # Declaring hyperparameters, activations, initializers etc.
    ##############################################################################
    
    # Assert "deterministic" behaviour for the experiments
    SEED = 2018
    tf.set_random_seed(SEED)
    
    # Dropout rate
    DRATE = 0.2
    
    WIDTHS = [500, 500, 2000, 10]
    
    # Encoder layer activations
    ENC_ACTS = ['relu', 'relu', 'relu', 'linear']
    # Decoder layer activations
    DEC_ACTS = ['relu', 'relu', 'relu', 'linear']
    
    # Weight initializers
    from tensorflow import truncated_normal_initializer as normal_init
    #  from tensorflow.contrib.layers import variance_scaling_initializer as var_init
    
    W_INIT = normal_init(mean=0.0, stddev=0.01, seed=SEED)
    #  W_INIT = var_init(factor=1./3., mode='FAN_IN', uniform=True)
    
    # Training hyperparameters (SGD)
    #  MOMENTUM = 0.9
    #  LEARNING_RATE = 0.1
    #  LAYERWISE_EPOCHS = 173
    #  LAYERWISE_LRD_EPOCHS = 73
    #  END2END_EPOCHS = 366
    #  END2END_LRD_EPOCHS = 173
    #  BATCH_SIZE = 256
    
    # Training hyperparameters (Adam)
    LAYERWISE_EPOCHS = 30
    END2END_EPOCHS = 30
    BATCH_SIZE = 256
    
    
    # Learning rate decay callback
    #  layer_decaySchedule=decay_lr(LAYERWISE_LRD_EPOCHS, 0.1)
    #  e2e_decaySchedule=decay_lr(END2END_LRD_EPOCHS, 0.1)
    
    
    # Load data
    try:
        data = np.load(sys.argv[1])
        # Dynamically retrieve the number of features in given dataset
        IN_FEATURES = data.shape[1]
        perm = np.random.permutation(data.shape[0])
        data = data[perm]
    except:
        mnist = load_mnist(val_size=0)
        data = np.concatenate((mnist.train.images, mnist.test.images))
        # Dynamically retrieve the number of features in given dataset
        IN_FEATURES = data.shape[1]
        perm = np.random.permutation(data.shape[0])
        data = data[perm]
    
    
    ##############################################################################
    # Neural network topology initialization
    ##############################################################################
    
    # End to end Autoencoder model
    e2e = tf.keras.models.Sequential()
    
    # Input layer (End to end Autoencoder)
    e2e_in = tf.keras.layers.InputLayer(input_shape=(IN_FEATURES,))
    e2e.add(e2e_in)
    
    # Encoder layers (End to end Autoencoder)
    for i, w in enumerate(WIDTHS):
        enc = tf.keras.layers.Dense(units=w, activation=ENC_ACTS[i],
                                    kernel_initializer=W_INIT)
        e2e.add(enc)
    
    # Decoder layers (End to end Autoencoder)
    for i, w in enumerate(reversed(WIDTHS[:-1])):
        e2e.add(tf.keras.layers.Dense(units=w, activation=DEC_ACTS[i],
                                      kernel_initializer=W_INIT))
    
    # Output layer (End to end Autoencoder)
    i += 1
    e2e.add(tf.keras.layers.Dense(units=IN_FEATURES, activation=DEC_ACTS[i],
                                  kernel_initializer=W_INIT))
    
    # If pre trained weights exist, dont train
    if os.path.exists('sae.h5'):
        e2e.load_weights('sae.h5')
    
        # Load dataset labels
        try:
            ground_truth = np.load(sys.argv[2])
            ground_truth = ground_truth[perm]
        except:
            ground_truth = np.concatenate((mnist.train.labels, mnist.test.labels))
            ground_truth = ground_truth[perm]
    
        eval_acc(e2e_in, enc, data, ground_truth, n_clusters=10, SEED=SEED)
        vis_2d_distributions(e2e_in, enc, data, ground_truth, flag='PCA')
    
    # Train and save model weights
    else:
        # Define training (End to end Autoencoder)
        #  e2e.compile(loss='mse',
                    #  optimizer=tf.keras.optimizers.SGD(lr=LEARNING_RATE,
                                                      #  momentum=MOMENTUM))
        e2e.compile(loss='mse',
                    optimizer=tf.keras.optimizers.Adam())
    
    
        ##########################################################################
        # Layerwise autoencoders topology and training (Practicing sharing layers)
        ##########################################################################
    
        # Hidden output tensor initialize
        HIDDEN_OUT = None
        # Input layer dataset initialize
        LAEW_IN = data
        # Number of layerwise autoencoders
        LAE_NUM = len(WIDTHS)
        
        # Log running state
        print 'Starting layerwise training.....'
    
        # Loop through widths that define each layerwise autoencoder
        for i, w in enumerate(WIDTHS):
            # First layerwise autoencoder (connected directly to Input/Output)
            if i == 0:
                # 1st Layerwise autoencoder model
                layerw_ae = tf.keras.models.Sequential()
                # Input layer (1st Layerwise Autoencoder)
                layerw_ae.add(e2e_in)
                # Dropout
                layerw_ae.add(tf.keras.layers.Dropout(rate=DRATE, seed=SEED))
                # Hidden layer (1st Layerwise Autoencoder)
                layerw_hidden = e2e.get_layer('dense_1')
                layerw_ae.add(e2e.get_layer('dense_1'))
                # Output layer (1st Layerwise Autoencoder)
                layerw_ae.add(e2e.get_layer('dense_8'))
    
                # Define training (1st Layerwise Autoencoder)
                #  layerw_ae.compile(loss='mse',
                                  #  optimizer=tf.keras.optimizers.SGD(lr=LEARNING_RATE,
                                                                    #  momentum=MOMENTUM))
                layerw_ae.compile(loss='mse',
                                  optimizer=tf.keras.optimizers.Adam())
                # Train (1st Layerwise Autoencoder)
                layerw_ae.fit(LAEW_IN, LAEW_IN,
                              batch_size=BATCH_SIZE,
                              epochs=LAYERWISE_EPOCHS,
                              #  callbacks=[layer_decaySchedule],
                              verbose=1)
            else:
                # i-th Layerwise autoencoder model
                layerw_ae = tf.keras.models.Sequential()
                # Input layer (i-th Layerwise Autoencoder)
                layerw_in = tf.keras.layers.InputLayer(
                    input_shape=(LAEW_IN.shape[-1],))
                layerw_ae.add(layerw_in)
                # Dropout
                layerw_ae.add(tf.keras.layers.Dropout(rate=DRATE, seed=SEED))
                # Hidden layer (i-th Layerwise Autoencoder)
                layerw_hidden = e2e.get_layer('dense_' + str(i + 1))
                layerw_ae.add(layerw_hidden)
                # Output layer (i-th Layerwise Autoencoder)
                layerw_ae.add(e2e.get_layer('dense_' + str(LAE_NUM * 2 - i)))
    
                # Define training (i-th Layerwise Autoencoder)
                #  layerw_ae.compile(loss='mse',
                                  #  optimizer=tf.keras.optimizers.SGD(lr=LEARNING_RATE,
                                                                    #  momentum=MOMENTUM)
                                  #  )
                layerw_ae.compile(loss='mse',
                                  optimizer=tf.keras.optimizers.Adam())
                # Train (i-th Layerwise Autoencoder)
                layerw_ae.fit(LAEW_IN, LAEW_IN,
                              batch_size=BATCH_SIZE,
                              epochs=LAYERWISE_EPOCHS,
                              #  callbacks=[layer_decaySchedule],
                              verbose=1)
    
            # Define pseudo model to get intermidiate layer output
            HIDDEN_OUT = tf.keras.models.Model(inputs=e2e_in.input,
                                               outputs=layerw_hidden.output)
            # Get output value
            LAEW_IN = HIDDEN_OUT.predict(data)
    
        # Log running state
        print 'Starting end to end training.....'
    
        # Train (End to end Autoencoder)
        e2e.fit(data, data,
                batch_size=BATCH_SIZE,
                epochs=END2END_EPOCHS,
                #  callbacks=[e2e_decaySchedule],
                verbose=1)
    
        # Log running state
        print 'Finished training.....'
    
        # Save model weights
        e2e.save_weights('sae.h5')
    
        # Log running state
        print 'Saved layer weights.....'
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

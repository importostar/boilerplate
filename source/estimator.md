---
title: estimator
date: 2020-05-07
---
Example Python program estimator.py


## Code

Python example

       prediction = {
           "class":tf.argmax(input=logits, axis=1),
           "probabilities":tf.nn.softmax(logits,name = "softmax")
           }
    
       if mode == tf.estimator.ModeKeys.PREDICT:
           return tf.estimator.EstimatorSpec(mode=mode, predictions=predictions)
    
       loss = tf.losses.sparse_softmax_cross_entropy(
           labels = labels,
           logits = logits)
    
       if mode == tf.estimator.ModeKeys.TRAIN:
           optimizer = tf.train.GradientDescentOptimizer(learning_rate = 0.001)
           training_op = optimizer.minimize(
               loss = loss,
               global_step = tf.train.get_global_step())
           return tf.estimator.EstimatorSpec(mode=mode, loss=loss, train_op=training_op)
    ###########################      
        estimator = tf.estimator.Estimator(
            model_fn = lenet,        
            model_dir = "D:/Study/DeepLearning/TensorFlow/ckp")
    
        tensors_to_log = {"probabilities": "softmax"}
        logging_hook = tf.train.LoggingTensorHook(
          tensors=tensors_to_log, every_n_iter=50)
        
        train_func = tf.estimator.inputs.numpy_input_fn(
            x = {"x":train_image},
            y = train_labels,
            batch_size = 50,
            num_epochs=None,
            shuffle=True)
    
        estimator.train(
            input_fn = train_func,
            steps = 200000,
            hooks = [logging_hook])     

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

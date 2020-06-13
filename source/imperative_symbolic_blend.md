---
title: imperative_symbolic_blend
date: 2020-05-07
---
Example Python program imperative_symbolic_blend.py


## Classes

* ValueError: Attempt to convert a value (<DeferredTensor 'None' shape=(?, 256) dtype=float32>) with an unsupported type (<class 'tensorflow.python.keras.engine.base_layer.DeferredTensor'>) to a Tensor.

## Code

Python example

    ############################################################################
    # Case 1: inserting non-layer ops into a graph of layers
    ############################################################################
    
    input_1 = tf.keras.Input(shape=(3,))
    x = tf.keras.layers.Dense(4)(input_1)
    output = tf.exp(x)  # !!
    model = tf.keras.Model(input_1, output)
    
    ############################################################################
    # Case 2: symbolic model with non-feedable (value or variable) inputs
    ############################################################################
    
    input_1 = tf.keras.Input(shape=(3,))
    ones = tf.ones(shape=(4, 5))
    input_2 = tf.keras.Input(tensor=ones)  # !!
    x = tf.keras.layers.Dense(4)(input_1)
    output = tf.keras.add([x, ones])
    model = tf.keras.Model(input_1, output)
    
    ###################
    # A seq2seq model
    ###################
    
    # Define an input sequence and process it.
    encoder_inputs = Input(shape=(None, num_encoder_tokens))
    encoder = LSTM(latent_dim, return_state=True)
    encoder_outputs, state_h, state_c = encoder(encoder_inputs)
    # We discard `encoder_outputs` and only keep the states.
    encoder_states = [state_h, state_c]
    
    # Set up the decoder, using `encoder_states` as initial state.
    decoder_inputs = Input(shape=(None, num_decoder_tokens))
    # We set up our decoder to return full output sequences,
    # and to return internal states as well. We don't use the 
    # return states in the training model, but we will use them in inference.
    decoder_lstm = LSTM(latent_dim, return_sequences=True, return_state=True)
    decoder_outputs, _, _ = decoder_lstm(decoder_inputs,
                                         initial_state=encoder_states)
    decoder_dense = Dense(num_decoder_tokens, activation='softmax')
    decoder_outputs = decoder_dense(decoder_outputs)
    
    # Define the model that will turn
    # `encoder_input_data` & `decoder_input_data` into `decoder_target_data`
    model = Model([encoder_inputs, decoder_inputs], decoder_outputs)
    
    encoder_model = Model(encoder_inputs, encoder_states)
    
    decoder_state_input_h = Input(shape=(latent_dim,))
    decoder_state_input_c = Input(shape=(latent_dim,))
    decoder_states_inputs = [decoder_state_input_h, decoder_state_input_c]
    decoder_outputs, state_h, state_c = decoder_lstm(
        decoder_inputs, initial_state=decoder_states_inputs)
    decoder_states = [state_h, state_c]
    decoder_outputs = decoder_dense(decoder_outputs)
    decoder_model = Model(
        [decoder_inputs] + decoder_states_inputs,
        [decoder_outputs] + decoder_states)
    
    '''
    Current fails with the trace:
    
    Traceback (most recent call last):
      File "lstm_seq2seq.py", line 155, in <module>
        validation_split=0.2)
      File "/Library/Python/2.7/site-packages/tensorflow/python/keras/engine/training.py", line 1560, in fit
        validation_steps=validation_steps)
      File "/Library/Python/2.7/site-packages/tensorflow/python/keras/engine/training_eager.py", line 698, in fit_loop
        batch_size=batch_size)
      File "/Library/Python/2.7/site-packages/tensorflow/python/keras/engine/training_eager.py", line 250, in iterator_fit_loop
        model, x, y, sample_weights=sample_weights, training=True)
      File "/Library/Python/2.7/site-packages/tensorflow/python/keras/engine/training_eager.py", line 504, in _process_single_batch
        training=training)
      File "/Library/Python/2.7/site-packages/tensorflow/python/keras/engine/training_eager.py", line 89, in _model_loss
        outs, masks = model._call_and_compute_mask(inputs, **kwargs)
      File "/Library/Python/2.7/site-packages/tensorflow/python/keras/engine/network.py", line 856, in _call_and_compute_mask
        mask=masks)
      File "/Library/Python/2.7/site-packages/tensorflow/python/keras/engine/network.py", line 1052, in _run_internal_graph
        output_tensors = layer.call(computed_tensors, **kwargs)
      File "/Library/Python/2.7/site-packages/tensorflow/python/keras/layers/recurrent.py", line 2177, in call
        inputs, mask=mask, training=training, initial_state=initial_state)
      File "/Library/Python/2.7/site-packages/tensorflow/python/keras/layers/recurrent.py", line 706, in call
        input_length=timesteps)
      File "/Library/Python/2.7/site-packages/tensorflow/python/keras/backend.py", line 3133, in rnn
        outputs, _ = step_function(inputs[0], initial_states + constants)
      File "/Library/Python/2.7/site-packages/tensorflow/python/keras/layers/recurrent.py", line 693, in step
        output, new_states = self.cell.call(inputs, states, **kwargs)
      File "/Library/Python/2.7/site-packages/tensorflow/python/keras/layers/recurrent.py", line 1968, in call
        x_i + K.dot(h_tm1_i, self.recurrent_kernel[:, :self.units]))
      File "/Library/Python/2.7/site-packages/tensorflow/python/keras/backend.py", line 1367, in dot
        out = math_ops.matmul(x, y)
      File "/Library/Python/2.7/site-packages/tensorflow/python/ops/math_ops.py", line 1984, in matmul
        a = ops.convert_to_tensor(a, name="a")
      File "/Library/Python/2.7/site-packages/tensorflow/python/framework/ops.py", line 1028, in convert_to_tensor
        as_ref=False)
      File "/Library/Python/2.7/site-packages/tensorflow/python/framework/ops.py", line 1124, in internal_convert_to_tensor
        ret = conversion_func(value, dtype=dtype, name=name, as_ref=as_ref)
      File "/Library/Python/2.7/site-packages/tensorflow/python/framework/constant_op.py", line 228, in _constant_tensor_conversion_function
        return constant(v, dtype=dtype, name=name)
      File "/Library/Python/2.7/site-packages/tensorflow/python/framework/constant_op.py", line 178, in constant
        t = convert_to_eager_tensor(value, ctx, dtype)
      File "/Library/Python/2.7/site-packages/tensorflow/python/framework/constant_op.py", line 113, in convert_to_eager_tensor
        return ops.EagerTensor(value, context=handle, device=device, dtype=dtype)
    ValueError: Attempt to convert a value (<DeferredTensor 'None' shape=(?, 256) dtype=float32>) with an unsupported type (<class 'tensorflow.python.keras.engine.base_layer.DeferredTensor'>) to a Tensor.
    '''

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

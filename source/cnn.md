---
title: cnn
date: 2020-05-07
---
Example Python program cnn.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from keras.datasets import mnist
* from keras.utils import np_utils
* from keras.models import Sequential
* from keras.layers import Convolution2D
* from keras.layers import MaxPooling2D
* from keras.layers import Flatten
* from keras.layers import Dense
* from keras.layers import Activation

## Methods

* def load_data():
* def build_model():
* def main():

## Code

Python example

    # for mnist data
    from keras.datasets import mnist
    from keras.utils import np_utils
    
    # for CNN models
    from keras.models import Sequential
    from keras.layers import Convolution2D
    from keras.layers import MaxPooling2D
    from keras.layers import Flatten
    from keras.layers import Dense
    from keras.layers import Activation
    
    
    def load_data():
        (x_train, y_train), (x_test, y_test) = mnist.load_data()
        x_train = x_train.reshape(x_train.shape[0], 28, 28, 1)
        x_test = x_test.reshape(x_test.shape[0], 28, 28, 1)
        x_train = x_train.astype('float32')
        x_test = x_test.astype('float32')
        x_train = x_train / 255
        x_test = x_test / 255
    
        y_train = np_utils.to_categorical(y_train, 10)
        y_test = np_utils.to_categorical(y_test, 10)
    
        return (x_train, y_train), (x_test, y_test)
    
    
    def build_model():
    	model = Sequential()
    
    	# initializing CNN
    	model.add(Convolution2D(
    		input_shape=(28, 28, 1),
    		filters=64,
    		kernel_size=5,
    		strides=1,
    		padding='same',
    		data_format='channels_first'))
    	model.add(Activation('relu'))
    	model.add(MaxPooling2D(
    		pool_size=2,
    		strides=2,
    		padding='same',
    		data_format='channels_first'))
    
    	# Second convolutional layer
    	model.add(Convolution2D(
    		32, 
    		5, 
    		strides=1,
    		padding='same',
    		data_format='channels_first'))
    	model.add(Activation('relu'))
    	model.add(MaxPooling2D(
    		2,
    		2,
    		'same',
    		data_format='channels_first'))
    
    	# flatten
    	model.add(Flatten())
    
    	# fully connected networks
    	model.add(Dense(1024))
    	model.add(Activation('relu'))
    
    	model.add(Dense(10))
    	model.add(Activation('softmax'))
    
    	# summary CNN model
    	model.summary()
    
    	return model
    
    
    def main():
    	(x_train, y_train), (x_test, y_test) = load_data()
    
    	model = build_model()
    
    	# compiling the CNN
    	model.compile(
    		optimizer='adam',
    		loss='binary_crossentropy',
    		metrics=['accuracy'])
    
    	# start training
    	model.fit(
    		x_train,
    		y_train,
    		epochs=1,
    		batch_size=64)
    
    	score = model.evaluate(x_train, y_train)
    	print('\nTrain Accuracy: ', score)
    
    	score = model.evaluate(x_test, y_test)
    	print('\nTest Accuracy: ', score)
    
    
    if __name__ == '__main__':
    	main()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

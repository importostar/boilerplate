---
title: rnn
date: 2020-05-07
---
Example Python program rnn.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* ''' import the Keras libraries and packages '''
* from keras.models import Sequential
* from keras.layers import Dense
* from keras.layers import LSTM
* from keras.layers import Dropout
* from keras.layers import Activation
* ''' import the mnist for datasets '''
* from keras.datasets import mnist
* from keras.utils import np_utils

## Methods

* def load_data():
* def build_model():
* def main():

## Code

Python example

    ''' import the Keras libraries and packages '''
    from keras.models import Sequential
    from keras.layers import Dense
    from keras.layers import LSTM
    from keras.layers import Dropout
    from keras.layers import Activation
    
    ''' import the mnist for datasets '''
    from keras.datasets import mnist
    from keras.utils import np_utils
    
    
    def load_data():
        (x_train, y_train), (x_test, y_test) = mnist.load_data()
        x_train = x_train.reshape(-1, 28, 28)
        x_test = x_test.reshape(-1, 28, 28)
        x_train = x_train.astype('float32')
        x_test = x_test.astype('float32')
        x_train = x_train / 255
        x_test = x_test / 255
    
        y_train = np_utils.to_categorical(y_train, 10)
        y_test = np_utils.to_categorical(y_test, 10)
    
        return (x_train, y_train), (x_test, y_test)
    
    
    ''' build RNN model '''
    def build_model():
    	model = Sequential()
    
    	''' adding the first LSTM layer and some dropout regularisation '''
    	model.add(LSTM(
    		units=50,
    		return_sequences=True,
    		batch_input_shape=(None, 28, 28)))
    	model.add(Dropout(0.2))
    
    	''' adding a sceond LSTM layer and some dropout regularisation '''
    	model.add(LSTM(
    		units=50,
    		return_sequences=True))
    	model.add(Dropout(0.2))
    
    	''' adding a third LSTM layer and some dropout regularisation '''
    	model.add(LSTM(
    		units=50,
    		return_sequences=True))
    	model.add(Dropout(0.2))
    
    	''' adding a fourth LSTM layer and some dropout regularisation '''
    	model.add(LSTM(
    		units=50)) # default return_sequences is false
    	model.add(Dropout(0.2))
    
    	''' adding the output layer '''
    	model.add(Dense(units=10))
    	model.add(Activation('softmax'))
    
    	model.summary()
    
    	return model
    
    
    def main():
    	(x_train, y_train), (x_test, y_test) = load_data()
    
    	model = build_model()
    
    	model.compile(
    		optimizer='adam',
    		loss='mean_squared_error')
    
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

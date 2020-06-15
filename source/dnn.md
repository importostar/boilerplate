---
title: dnn
date: 2020-05-07
---
Example Python program dnn.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from keras.datasets import mnist
* from keras.utils import np_utils
* import numpy as np
* from keras.models import Sequential
* from keras.layers.core import Dense, Activation
* from keras.optimizers import Adam

## Methods

* def load_data():
* def build_model():
* def main():

## Code

Python example

    from keras.datasets import mnist
    from keras.utils import np_utils
    
    import numpy as np
    from keras.models import Sequential
    from keras.layers.core import Dense, Activation
    from keras.optimizers import Adam
    
    
    def load_data():
        (x_train, y_train), (x_test, y_test) = mnist.load_data()
        x_train = x_train.reshape(x_train.shape[0], 28*28)
        x_test = x_test.reshape(x_test.shape[0], 28*28)
        x_train = x_train.astype('float32')
        x_test = x_test.astype('float32')
        x_train = x_train / 255
        x_test = x_test / 255
    
        y_train = np_utils.to_categorical(y_train, 10)
        y_test = np_utils.to_categorical(y_test, 10)
    
        return (x_train, y_train), (x_test, y_test)
    
    
    ''' DNN Model '''
    def build_model():
        model = Sequential()
    
        model.add(Dense(input_dim=28*28, units=500, activation='relu'))
        model.add(Dense(units=500, activation='relu'))
        model.add(Dense(units=500, activation='relu'))
        model.add(Dense(units=10,activation='softmax'))
        model.summary()
        return model
    
    
    def main():
        (x_train, y_train), (x_test, y_test) = load_data()
        model = build_model()
        model.compile(loss='categorical_crossentropy', optimizer="adam", metrics=['accuracy'])
        model.fit(x_train, y_train, batch_size=100, epochs=20)
    
        score = model.evaluate(x_train, y_train)
        print("\nTrain Acc: ", score)
        score = model.evaluate(x_test, y_test)
        print("\nTest Acc: ", score[1])
    
    
    if __name__ == '__main__':
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

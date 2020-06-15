---
title: handwritten_digits
date: 2020-05-07
---
Example Python program handwritten_digits.py

## Modules

* import re
* import scipy.io
* import scipy.linalg
* import scipy.sparse.linalg;
* import numpy
* import matplotlib.pyplot

## Methods

* def relative_residual(U, z):

## Code

Python example

    import re
    import scipy.io
    import scipy.linalg
    import scipy.sparse.linalg;
    import numpy
    import matplotlib.pyplot
    
    def relative_residual(U, z):
        m, n = U.shape
        return numpy.linalg.norm((numpy.eye(m) - U.dot(U.T)).dot(z)) / numpy.linalg.norm(z)
    
    training_digits = scipy.io.loadmat('training_digits.mat')['azip']
    correct_training_digits = scipy.io.loadmat('correct_training_digits.mat')['dzip']
    test_digits = scipy.io.loadmat('test_digits.mat')['testzip']
    correct_test_digits = scipy.io.loadmat('correct_test_digits.mat')['dtest'][0]
    
    correct_training_digits_indicies = [[] for i in range(0,10)]
    for digit in range(0,10):
        for idx, val in enumerate(numpy.nditer(correct_training_digits)):
            if digit == int(val):
                correct_training_digits_indicies[int(val)].append(idx)
    
    training_set = [None] * 10
    for digit in range(0,10):
        training_set[digit] = training_digits[:,correct_training_digits_indicies[digit]]
    
    singular_values = [numpy.zeros((256,1)) for i in range(0,10)]
    matplotlib.pyplot.figure(1)
    for digit in range(0,10):
        s = scipy.linalg.svdvals(training_set[digit])
        for i in range(0,s.shape[0]):
            singular_values[digit][i] = s[i]
        matplotlib.pyplot.plot(range(0,256), singular_values[digit])
        matplotlib.pyplot.axis([1, 256, 0, 240])
        matplotlib.pyplot.hold(True)
    matplotlib.pyplot.hold(False)
    
    correct_predictions = numpy.zeros((10,16))
    for rank in range(5,21):
        U = [None] * 10
        s = [None] * 10
        Vh = [None] * 10
        for digit in range(0,10):
            U[digit], s[digit], Vh[digit] = scipy.sparse.linalg.svds(training_set[digit], k=rank)
        for i in range(0,test_digits.shape[1]):
            residuals = numpy.zeros(10)
            z = test_digits[:,i]
            for digit in range(0,10):
                residuals[digit] = relative_residual(U[digit], z)
    
            predicted_digit = numpy.argmin(residuals)
            if correct_test_digits[i] == predicted_digit:
                correct_predictions[predicted_digit][rank-5] += 1
    
    
    matplotlib.pyplot.figure(2)
    accuracy_k = numpy.zeros((16,))
    for rank in range(5,21):
        accuracy_k[rank-5] = numpy.sum(correct_predictions[:,rank-5]) / test_digits.shape[1]
    matplotlib.pyplot.plot(range(5,21), accuracy_k)
    
    matplotlib.pyplot.figure(3)
    accuracy_digit = numpy.zeros((10,))
    for digit in range(0,10):
        num_digits = numpy.where(correct_test_digits == digit)[0].__len__()
        accuracy_digit[digit] = numpy.sum(correct_predictions[digit,:]) / (16*num_digits)
    matplotlib.pyplot.plot(range(0,10), accuracy_digit)
    matplotlib.pyplot.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

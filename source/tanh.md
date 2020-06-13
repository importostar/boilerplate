---
title: tanh
date: 2020-05-07
---
Example Python program tanh.py

## Modules

* from numpy import *
* import scipy as sp
* from scipy import signal
* import matplotlib.pyplot as plt
* import matplotlib

## Methods

* def showAbsFFT(signal):
* def vox_fasttanh_ultra(X):
* def vox_fasttanh2( x ): 
* def juce_tanh( x ):

## Code

Python example

    # ref.: https://www.kvraudio.com/forum/viewtopic.php?t=388650&start=45
    # original.: https://nbviewer.jupyter.org/gist/JTriggerFish/6226363
    # added fast tanh of JUCE library
    
    from numpy import *
    import scipy as sp
    from scipy import signal
    import matplotlib.pyplot as plt
    %matplotlib inline
    import matplotlib
    #matplotlib.rcParams['savefig.dpi'] = 1 * matplotlib.rcParams['savefig.dpi']
    matplotlib.rcParams['figure.figsize'] = (20,5)
    
    N=4096
    factor=1
    
    f = 1./7.8
    
    t = linspace(0, N, N)
    freq = fft.fftfreq(N*factor, t.shape[-1])
    
    sine = sin(2*pi*f*t)
    saw  = sp.signal.sawtooth(2*pi*f*t)
    
    def showAbsFFT(signal):
        window = blackman(N)
        windowed = window*signal
        padded   = pad(windowed, (0, N*factor - N), 'constant', constant_values=(0))
        signalX = fft.fft(padded) / N
        amplX = abs(signalX)
        plt.plot(freq[0:int(len(padded)/2)], 20*log(amplX)[0:int(len(padded)/2)])
        
    showAbsFFT(sine)
    
    def vox_fasttanh_ultra(X):
       ax = fabs( X ); 
       x2 = X * X; 
       Z = X * ( 0.773062670268356 + ax + 
          ( 0.757118539838817 + 0.0139332362248817 * x2 * x2 ) * 
          x2 * ax ); 
    
       return( Z / ( 0.795956503022967 + fabs( Z )))
    
    def vox_fasttanh2( x ): 
       ax = fabs( x ); 
       x2 = x * x; 
    
       return( x * ( 2.45550750702956 + 2.45550750702956 * ax + 
          ( 0.893229853513558 + 0.821226666969744 * ax ) * x2 ) / 
          ( 2.44506634652299 + ( 2.44506634652299 + x2 ) * 
          fabs( x + 0.814642734961073 * x * ax ))); 
    
    def juce_tanh( x ):
        x2 = x * x;
        numerator = x * (-135135 + x2 * (17325 + x2 * (-378 + x2)));
        denominator = -135135 + x2 * (62370 + x2 * (-3150 + 28 * x2));
        return numerator / denominator;
    
    showAbsFFT(tanh(sine))
    showAbsFFT(vox_fasttanh_ultra(sine))
    showAbsFFT(vox_fasttanh2(sine))
    showAbsFFT(juce_tanh(sine))

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

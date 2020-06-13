---
title: eeg_to_spectrogram
date: 2020-05-07
---
Example Python program eeg_to_spectrogram.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import pyedflib
* import numpy as np
* import matplotlib
* import matplotlib.pyplot as plt
* from matplotlib.pyplot import specgram
* from scipy.signal import spectrogram

## Code

Python example

    # eeg_to_spectrogram
    
    # steps
    
    # 1. read eeg with pyedflib
    # 2. convert eeg signal to spectrogram using matplotlib
    # 3. remove unneccesary staff from matplotlib
    # 4. save a pure spectrogram image for further analysis or 
    # machine learning image classification task
    
    # reference
    # https://dsp.stackexchange.com/questions/25115/python-time-frequency-spectrogram
    # https://stackoverflow.com/questions/11837979/removing-white-space-around-a-saved-image-in-matplotlib
    
    import pyedflib
    import numpy as np
    import matplotlib
    import matplotlib.pyplot as plt
    from matplotlib.pyplot import specgram
    
    f = pyedflib.EdfReader("data/shhs1-200001.edf")
    a = (f.readSignal(2))
    print(a.shape)
    
    # use scipy.signal spectrogram to extract raw data
    from scipy.signal import spectrogram
    raw = spectrogram(a[:7500], fs=125, noverlap=1)[2]
    
    im = specgram(a[:7500], Fs=125, noverlap=1)[3]
    plt.gca().set_axis_off()
    plt.subplots_adjust(top = 1, bottom = 0, right = 1, left = 0, 
                hspace = 0, wspace = 0)
    plt.margins(0,0)
    plt.gca().xaxis.set_major_locator(matplotlib.ticker.NullLocator())
    plt.gca().yaxis.set_major_locator(matplotlib.ticker.NullLocator())
    plt.savefig("image.png", bbox_inches = 'tight',
        pad_inches = 0)
    f._close()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

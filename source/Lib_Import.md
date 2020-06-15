---
title: Lib_Import
date: 2020-05-07
---
Example Python program Lib_Import.py

## Modules

* import os, sys
* import time, json, csv
* from glob import glob
* import numpy as np
* import pandas as pd
* import torch
* import torch.nn as nn
* import torch.nn.functional as F
* from torch.utils.data import DataLoader, Dataset
* from platform import system
* import matplotlib
* import matplotlib.pyplot as plt
* import cv2
* from PIL import Image
* import torchvision
* import torchvision.transforms as transforms
* from gensim.models import word2vec
* # import torchaudio
* # import librosa
* from tqdm import tqdm
* from pprint import pprint

## Code

Python example

    import os, sys
    import time, json, csv
    from glob import glob
    
    import numpy as np
    import pandas as pd
    
    # %% 深度學習套件 deep learning related 
    import torch
    import torch.nn as nn
    import torch.nn.functional as F
    from torch.utils.data import DataLoader, Dataset
    
    # %% 視覺化/製圖套件 visualization / plotting
    # MacOSX 比較麻煩⋯⋯
    from platform import system
    if system() == "Darwin":
        import matplotlib
        matplotlib.use('TkAgg')
    
    import matplotlib.pyplot as plt
    
    # %% 圖片處理套件 CV related
    import cv2
    from PIL import Image
    import torchvision
    import torchvision.transforms as transforms
    
    # %% 文字處理套件 NLP related
    from gensim.models import word2vec
    
    # %% 音訊處理套件 Speech related
    # import torchaudio
    # import librosa
    
    # %% 好用的進度條和排版工具
    ##   progress bar and pretty print
    from tqdm import tqdm
    from pprint import pprint

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

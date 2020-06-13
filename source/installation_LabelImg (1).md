---
title: installation_LabelImg (1)
date: 2020-05-07
---
Example Python program installation_LabelImg (1).py


## Code

Example Python PyQt program :

    Ubuntu Linux
    Python 2 + Qt4
    
    sudo apt-get install pyqt4-dev-tools
    sudo pip install lxml
    make qt4py2
    python labelImg.py
    python labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
    Python 3 + Qt5 (Recommended)
    
    sudo apt-get install pyqt5-dev-tools
    sudo pip3 install -r requirements/requirements-linux-python3.txt
    make qt5py3
    python3 labelImg.py
    python3 labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
    macOS
    Python 2 + Qt4
    
    brew install qt qt4
    brew install libxml2
    make qt4py2
    python labelImg.py
    python labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
    Python 3 + Qt5 (Recommended)
    
    brew install qt  # Install qt-5.x.x by Homebrew
    brew install libxml2
    
    or using pip
    
    pip3 install pyqt5 lxml # Install qt and lxml by pip
    
    make qt5py3
    python3 labelImg.py
    python3 labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
    Python 3 Virtualenv (Recommended)
    
    Virtualenv can avoid a lot of the QT / Python version issues
    
    brew install python3
    pip3 install pipenv
    pipenv run pip install pyqt5==5.13.2 lxml
    pipenv run make qt5py3
    python3 labelImg.py
    [Optional] rm -rf build dist; python setup.py py2app -A;mv "dist/labelImg.app" /Applications

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

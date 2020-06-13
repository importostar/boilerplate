---
title: install_opencv_raspberry_pi3
date: 2020-05-07
---
Example Python program install_opencv_raspberry_pi3.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import cv2

## Code

Example Python PyQt program :

    ### バージョンチェック ###
    python3
    import cv2
    cv2.__version__
    print(cv2.getBuildInformation())
    
    
    ### 依存パッケージのインストール ###
    # 古いイメージだと、1回目のupdateでエラーが出るかも。気にせずupgradeして、再度update,upgradesudo する
    sudo apt update
    sudo apt upgrade
    sudo apt update
    sudo apt upgrade
    
    sudo apt -y install cmake cmake-curses-gui
    sudo apt -y install python3-dev python3-pip
    sudo apt -y install libtbb-dev
    sudo apt -y install libhdf5-dev libhdf5-serial-dev  gfortran libtesseract-dev libleptonica-dev  libatlas-base-dev liblapacke-dev 
    sudo apt -y install libeigen3-dev
    sudo apt -y install libjpeg8-dev libjasper-dev libpng12-dev
    sudo apt -y install libtiff5-dev libtiff-dev
    sudo apt -y install ffmpeg
    sudo apt -y install libavcodec-dev libavformat-dev libswscale-dev libdc1394-22-dev libavresample-dev 
    sudo apt -y install libvorbis-dev libxvidcore-dev libx264-dev libxvidcore-dev
    sudo apt -y install libopencore-amrnb-dev libopencore-amrwb-dev
    sudo apt -y install libxine2-dev libv4l-dev
    sudo apt -y install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev gstreamer1.0-plugins-*
    sudo apt -y install libgtk2.0-dev
    sudo apt -y install libgtk-3-dev  libcanberra-gtk*
    # sudo apt -y install libqtgui4 libqtwebkit4 libqt4-test libqt4-dev libqt4-opengl-dev python3-pyqt5
    
    ## workaround for libhdf5 ##
    sudo ln -s /usr/lib/arm-linux-gnueabihf/libhdf5_serial.so /usr/lib/arm-linux-gnueabihf/libhdf5.so
    sudo ln -s /usr/lib/arm-linux-gnueabihf/libhdf5_serial_hl.so /usr/lib/arm-linux-gnueabihf/libhdf5_hl.so
    
    
    ## お手軽 for Python only
    # sudo pip3 --default-timeout=1000 install opencv-python
    
    
    ### Swapの増加 ###
    swapon
    sudo sed -i -e 's/SWAPSIZE=.*/SWAPSIZE=2048/g' /etc/dphys-swapfile
    sudo systemctl restart dphys-swapfile.service
    swapon
    
    
    ### OpenCVコードの取得 ###
    cd ~/
    mkdir work
    cd work
    
    cvVersion="4.1.0"
    
    git clone https://github.com/opencv/opencv.git
    cd opencv
    git checkout $cvVersion
    cd ..
    
    ### opencv_contribもビルドしたい場合 ###
    # git clone https://github.com/opencv/opencv_contrib.git
    # cd opencv_contrib
    # git checkout $cvVersion
    # cd ..
    # CMakeに↓を追加
    #    -D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules \
    
    ### Openビルド設定 ###
    cd ~/work/opencv
    mkdir build
    cd build
    
    cmake \
        -D CMAKE_BUILD_TYPE=RELEASE \
        -D CMAKE_INSTALL_PREFIX=/usr/local \
        -D OPENCV_GENERATE_PKGCONFIG=ON \
        -D ENABLE_VFPV3=ON \
        -D ENABLE_NEON=ON \
        -D WITH_TBB=ON \
        -D WITH_V4L=ON \
        -D WITH_GSTREAMER=ON \
        -D WITH_FFMPEG=ON \
        -D WITH_QT=OFF \
        -D WITH_GTK=ON \
        -D WITH_GTK3=ON \
        ..
    
    ### OpenCVビルド、インストール ###
    make -j4
    sudo make install
    sudo ldconfig
    
    ### Swapを戻す ###
    swapon
    sudo sed -i -e 's/SWAPSIZE=.*/SWAPSIZE=256/g' /etc/dphys-swapfile
    sudo systemctl restart dphys-swapfile.service
    swapon
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

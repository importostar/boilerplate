---
title: start (1)
date: 2020-05-07
---
Example Python program start (1).py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import getpass
* import os
* from sys import exit, platform, argv
* from PyQt5 import QtCore, QtGui, QtWidgets
* from PyQt5.QtWidgets import QApplication, QWidget, QComboBox, QPushButton, QRadioButton, QLabel, QLineEdit, QMessageBox, \
* import main

## Methods

* def btn_rad():
* def get_path():
* def brows():
* def start_(url='', typos=''):
* def start_s(url=""):
* def about():

## Code

Example Python PyQt program :

    import getpass
    import os
    from sys import exit, platform, argv
    from PyQt5 import QtCore, QtGui, QtWidgets
    from PyQt5.QtWidgets import QApplication, QWidget, QComboBox, QPushButton, QRadioButton, QLabel, QLineEdit, QMessageBox, \
        QFileDialog
    import main
    
    d = main.downloader()
    user = getpass.getuser()
    print(user)
    if platform == 'win32':
        path = 'C:\\Users\\' + user + '\\Videos'
    else:
        path = os.getcwd()
    print(path)
    
    app = QApplication(argv)
    main_window = QWidget()
    main_window.setWindowTitle("Video Downloader")
    main_window.setFixedSize(500, 200)
    main_window.resize(400, 150)
    icon = QtGui.QIcon()
    icon.addPixmap(QtGui.QPixmap("./youtube.ico"), QtGui.QIcon.Normal, QtGui.QIcon.Off)
    main_window.setWindowIcon(icon)
    main_window.setStyleSheet("background-color:white;")
    
    exit_btn = QPushButton("Exit", main_window)
    exit_btn.clicked.connect(exit)
    exit_btn.move(400, 160)
    exit_btn.setStyleSheet("padding:10px;border:1px solid orange;color:red;")
    
    combo = QComboBox(main_window)
    combo.move(200, 15)
    combo.addItem("1440p")
    combo.addItem("1080p")
    combo.addItem("720p")
    combo.addItem("480p")
    combo.addItem("360p")
    combo.addItem("240p")
    combo.addItem("144p")
    combo.setStyleSheet("border:1px solid orange;padding:3px;color:green;")
    
    combo1 = QComboBox(main_window)
    combo1.move(300, 15)
    combo1.addItem("mp4")
    combo1.addItem("webm")
    combo1.addItem("3gpp")
    combo1.setStyleSheet("border:1px solid orange;padding:3px;color:green;")
    
    
    def btn_rad():
        combo.setEnabled(not audios.isChecked())
    
    
    audios = QRadioButton(main_window)
    audios.setText("Audio")
    var = audios.toggled.connect(btn_rad)
    audios.move(400, 20)
    audios.setStyleSheet("color:green;")
    
    choose = QLabel(main_window, text="<b>Choose video Format :</b>")
    choose.move(10, 20)
    choose.setStyleSheet("color:green")
    
    link = QLineEdit(main_window)
    link.setPlaceholderText("past the line here ")
    link.resize(400, 30)
    link.move(10, 70)
    link.setStyleSheet("border:1px solid blue;padding:3px;color:gray;")
    
    
    def get_path():
        global path
        path = ""
        path = QFileDialog.getSaveFileName(main_window, 'save video at', 'video.mp4')
        path = str(path)
        if path != "('', '')":
            platforms = platform
            print(path)
            print(platforms)
            if platforms == 'linux':
                path_1 = path
                path_1 = path_1.split('/')
                print(path_1)
                name = path_1[-1]
                path = path.replace(name, '')
            else:
                path = os.path.split(os.path.abspath(path))[0]
                path = path.split("\('")[1]
    
            print(path)
    
    
    save_button = QPushButton("...", main_window)
    save_button.resize(40, 30)
    save_button.move(430, 70)
    save_button.clicked.connect(get_path)
    save_button.setStyleSheet("background-color:orange;border:1px solid orange;padding:3px;color:white")
    
    
    def brows():
        global path
        paths = QFileDialog.getOpenFileName(main_window, 'open video at', filter="*.txt")
        paths = str(paths)
        print(str(paths))
        if paths != "('', '')":
            paths = paths.split(",")[0]
            path = os.path.split(os.path.abspath(paths))[0]
            path = path.split("('")[1]
            paths = paths[1:].replace("/", "\\")
            paths = paths.replace("'", "")
            print(paths)
            vd = open(str(paths), "r")
            t = 0
            for v in vd:
                start_(v, 'quick')
                t += 1
                print(t)
    
    
    brows_button = QPushButton("Past", main_window)
    brows_button.resize(40, 30)
    brows_button.move(30, 40)
    brows_button.clicked.connect(brows)
    brows_button.setStyleSheet("background-color:green;margin:1px;color:white;border:1px solid green")
    
    
    def start_(url='', typos=''):
        global audio
        fil_ext = str(combo1.currentText())
        audio = audios.isChecked()
        if not url:
            url = link.text()
        if url == "":
            msg_1 = """Please Enter url"""
            QMessageBox.warning(main_window, 'No Video Found', msg_1, QMessageBox.Ok)
        else:
            if str(url).find("youtu.be") == 8 or str(url).find("https://www.youtube.com/watch?v=") == 0:
                print(str(url).find("youtu.be"))
                video_quality = str(combo.currentText())
                video_type = video_quality
                print("start")
                place = path
                msgs = d.start_downloader(url, video_type, fil_ext, place, audio)
                print(msgs)
                if not typos or msgs == "wrong link or no internet and bad connection":
                    QMessageBox.information(main_window, 'Download finish', msgs, QMessageBox.Ok)
            else:
                QMessageBox.information(main_window, 'Unknown url', ' the video site not supported',
                                        QMessageBox.Ok)
    
    
    download_button = QPushButton("Start Download", main_window)
    download_button.move(170, 110)
    download_button.setStyleSheet("background-color: blue;padding:5px;color:white;border:1px solid blue")
    download_button.clicked.connect(start_)
    
    
    def start_s(url=""):
        if not url:
            url = link.text()
        if not url:
            msg = """Please Enter url"""
            QMessageBox.warning(main_window, 'No Video Found', msg, QMessageBox.Ok)
        else:
            if str(url).find("https://www.youtube.com/playlist?list=") == 0:
                msgs = d.start_playlist(url)
                if not msgs:
                    QMessageBox.information(main_window, 'Download finish', 'Download Finished',
                                            QMessageBox.Ok)
            else:
                QMessageBox.information(main_window, 'Unknown url', ' the video site not supported',
                                        QMessageBox.Ok)
    
    
    download_button1 = QPushButton("Download Playlist", main_window)
    download_button1.move(50, 110)
    download_button1.setStyleSheet("background-color: red;padding:5px;color:white;border:1px solid red")
    download_button1.clicked.connect(start_s)
    
    
    def about():
        msg = """
        This program create by Arkan Leki
        For any Information or get the source code
        ask me on fb.com/arkan.leki"""
        QMessageBox.information(main_window, 'About', msg, QMessageBox.Ok)
    
    
    about_button = QPushButton("About", main_window)
    about_button.move(300, 160)
    about_button.clicked.connect(about)
    about_button.setStyleSheet("padding:10px;border:1px solid orange;color:green;")
    
    main_window.show()
    exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

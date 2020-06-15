---
title: Lesson8All
date: 2020-05-07
---
Example Python program Lesson8All.py
This program creates a PyQt GUI

## Modules

* import sys,os
* import PyQt5.QtGui as QtGui
* import PyQt5.QtCore as QtCore
* from PyQt5.QtWidgets import (QApplication, QWidget, QMainWindow,QCheckBox,QSlider,
* import cv2
* import numpy as np

## Classes

* class Pane01(QWidget):
* class Pane02(QWidget):
* class Pane03(QWidget):

## Methods

* def cv2qtPixmap(cv2img):
* def __init__(self, parent=None):
* def initial(self):
* def do_open(self):
* def do_show(self,p,tmpimg):
* def do_gray(self,cimg):
* def do_thres(self,gimg):
* def do_setThres(self,val):
* def do_setThresAndShow(self,val):
* def setGray(self,val):
* def __init__(self, parent=None):
* def initial(self):
* def __init__(self, parent=None):
* def initial(self):
* def main():

## Code

Example Python PyQt program :

    import sys,os
    import PyQt5.QtGui as QtGui
    import PyQt5.QtCore as QtCore
    from PyQt5.QtWidgets import (QApplication, QWidget, QMainWindow,QCheckBox,QSlider,
                                 QGridLayout, QVBoxLayout, QHBoxLayout,QSpinBox,
                                 QLabel, QLineEdit, QPushButton, QFileDialog)
    import cv2
    import numpy as np
    
    # OpenCV2 の画像から　Qt5 のpixmapを生成する関数
    def cv2qtPixmap(cv2img):
        height, width, dim = cv2img.shape
        bytesPerLine = dim * width
        rgbimg = cv2.cvtColor(cv2img,cv2.COLOR_BGR2RGB)
        qtimg = QtGui.QImage(rgbimg.data,width,height,bytesPerLine,QtGui.QImage.Format_RGB888)
        pixmap = QtGui.QPixmap.fromImage(qtimg)
        return pixmap
    
    # ウィンドウの上部エリア
    class Pane01(QWidget):
        def __init__(self, parent=None):
            QWidget.__init__(self, parent=parent)
            self.initial()
    
        # 文字列を送信する独自 SIGNAL pathset_signal を定義
        pathset_signal = QtCore.pyqtSignal(str)
    
        def initial(self):
            # 512x512の真っ黒のダミー画像を作る
            dummypixmap = cv2qtPixmap(np.zeros((512,512,3),dtype=np.uint8))
            # Label Widget に画像を貼り付ける．Labelを表示すれば画像が表示される
            self.imagePane = QLabel(u"パネル",parent=self)
            self.imagePane.setPixmap(dummypixmap)
            self.imagePane2 = QLabel(u"パネル",parent=self)
            self.imagePane2.setPixmap(dummypixmap)
    
            # 自動水平レイアウトで 上記Widetを配置したレイアウトをつくる
            self.layout = QHBoxLayout()
            self.setLayout(self.layout)
            self.layout.addWidget(self.imagePane)
            self.layout.addWidget(self.imagePane2)
    
            self.do_setThres(127)
            self.srcimg = np.zeros((512,512,3),dtype=np.uint8)
            self.gryimg = self.do_gray(self.srcimg)
            self.grayflag = False
    
        def do_open(self):
            self.path,_ = QFileDialog.getOpenFileName(self,"Open File")
            self.srcimg = cv2.imread(self.path)
            self.do_show(1,self.srcimg)
            self.gryimg = self.do_gray(self.srcimg)
            self.do_show(2,self.do_thres(self.gryimg))
            # ファイル名を載せてど独自シグナル pathset_signal を発信
            self.pathset_signal.emit(self.path)
    
        def do_show(self,p,tmpimg):
            if tmpimg.shape[0]>tmpimg.shape[1]:
                self.cv2image = cv2.resize(tmpimg,(int(512*tmpimg.shape[1]/tmpimg.shape[0]),512))
            else:
                self.cv2image = cv2.resize(tmpimg,(512,int(512*tmpimg.shape[0]/tmpimg.shape[1])))
            if self.grayflag :
               pixmap = cv2qtPixmap(
                   cv2.cvtColor(cv2.cvtColor(self.cv2image,cv2.COLOR_BGR2GRAY),cv2.COLOR_GRAY2BGR))
            else:
               pixmap = cv2qtPixmap(self.cv2image)
            if p==1:
                self.imagePane.setPixmap(pixmap)
            else:
                self.imagePane2.setPixmap(pixmap)
    
     # グレイ画像の生成
        def do_gray(self,cimg):
            tmpgryimg = cv2.cvtColor(cimg,cv2.COLOR_BGR2GRAY)
            return tmpgryimg
        # 2階調化した後、表示用にBGR画像に変換して返す
        def do_thres(self,gimg):
            v,tmpimg = cv2.threshold(gimg,self.Thres,255,cv2.THRESH_BINARY)
            return cv2.cvtColor(tmpimg,cv2.COLOR_GRAY2BGR)
        # しきい値の設定
        def do_setThres(self,val):
            self.Thres = val
        # しきい値を設定し、２階調化し、表示
        def do_setThresAndShow(self,val):
            self.do_setThres(val)
            self.do_show(2,self.do_thres(self.gryimg))
        # グレー表示フラグのセット関数
        def setGray(self,val):
            if val :
                self.grayflag = True;
            else:
                self.grayflag = False;
            self.do_show(1,self.srcimg)
    
    # ウィンドウの下部エリア
    class Pane02(QWidget):
        def __init__(self, parent=None):
            QWidget.__init__(self, parent=parent)
            self.initial()
    
        def initial(self):
            # ボタンWidgetを一つ作る
            self.fopenButton = QPushButton(u"開く",parent=self)
            # ボタンWidgetを一つ作る
            self.quitButton = QPushButton(u"終了",parent=self)
            # 自動水平レイアウトで 上記Widetを配置したレイアウトをつくる
            layout = QHBoxLayout()
            self.setLayout(layout)
            layout.addWidget(self.fopenButton)
            layout.addWidget(self.quitButton)
    
    class Pane03(QWidget):
        def __init__(self, parent=None):
            QWidget.__init__(self, parent=parent)
            self.initial()
    
        def initial(self):
            # チェックボックス default は unchecked
            self.grayBox = QCheckBox(parent=self)
            # ラベル
            self.tresL = QLabel(u"しきい値",parent=self)
            # スピンボックス
            self.spinBox = QSpinBox(parent=self)
            self.spinBox.setRange(0,255)
            self.spinBox.setValue(127)
            # スライダー
            self.slider = QSlider(QtCore.Qt.Horizontal,parent=self)
            self.slider.setRange(0,255)
            self.slider.setValue(127)
            # 1行の入力用テキストボックス
            self.textEdit = QLineEdit(u"ABC",parent=self)
    
            # 自動水平レイアウトで 上記Widetを配置したレイアウトをつくる
            layout = QHBoxLayout()
            self.setLayout(layout)
            layout.addWidget(self.grayBox)
            layout.addWidget(self.tresL)
            layout.addWidget(self.spinBox)
            layout.addWidget(self.slider)
            layout.addWidget(self.textEdit)
    
            # スピンボックスとスライダを同期
            self.spinBox.valueChanged.connect(self.slider.setValue)
            self.slider.valueChanged.connect(self.spinBox.setValue)
    
    def main():
        # 次の3行はおきまり
        app = QApplication(sys.argv)
        mainWindow = QMainWindow()
        mainPanels = QWidget()
    
        # 自動垂直レイアウトに Pane01,Pane02 のインスタンスを貼り付ける
        layout = QVBoxLayout()
        pane01 = Pane01(parent=mainPanels)
        layout.addWidget(pane01)
        pane03 = Pane03(parent=mainPanels)
        layout.addWidget(pane03)
        pane02 = Pane02(parent=mainPanels)
        layout.addWidget(pane02)
    
        # fopenButton のクリックいベントに do_open 関数をアタッチ
        pane02.fopenButton.clicked.connect(pane01.do_open)
        pane02.quitButton.clicked.connect(app.quit)
        pane03.slider.valueChanged.connect(pane01.do_setThresAndShow)
        pane03.grayBox.stateChanged.connect(pane01.setGray)
        # 独自シグナル pathse_signal と textEdit の setText スロットを連結
        pane01.pathset_signal.connect(pane03.textEdit.setText)
    
        # メインパネルにレイアウトしたものを貼り付ける
        mainPanels.setLayout(layout)
        # メインパネルをウィンドウ中央エリアに取り付け
        mainWindow.setCentralWidget(mainPanels)
    
        #　最後に表示してプログラムを実行　この2行はおきまり
        mainWindow.show()
        app.exec_()
    
    if __name__ == '__main__':
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

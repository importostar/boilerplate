---
title: db_stock_test (1)
date: 2020-05-07
---
Example Python program db_stock_test (1).py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5.QtCore import pyqtSlot, pyqtSignal, QObject
* from PyQt5.QtWidgets import *
* from PyQt5.QAxContainer import *
* import ctypes
* import sys

## Classes

* class DBFI(QAxWidget):
* class MyMain(QWidget):

## Methods

* def __init__(self):
* def login(self):
* def logout(self):
* def _onconnected(self, api_handle):
* def _ondisconnected(self):
* def _receive_tr_data(self, sender, data):
* def _receive_real_data(self, name, field, data):
* def get_login_info(self):
* def get_real_data(self):
* def end_real_data(self):
* def __init__(self):
* def btn1_clicked(self):
* def btn2_clicked(self):
* def __btn3_clicked(self):
* def __btn4_clicked(self):
* def __btn5_clicked(self):

## Code

Example Python PyQt program :

    """
    DB금융투자
    """
    from PyQt5.QtCore import pyqtSlot, pyqtSignal, QObject
    from PyQt5.QtWidgets import *
    from PyQt5.QAxContainer import *
    
    import ctypes
    
    ID_ADVICE_RT = -73    # 실시간 데이타 등록
    ID_UNADVICE_RT = -74   # 실시간 데이타 등록해제
    
    R_S31 = "S31"  # 주식/ETF 현재가
    R_X12 = "X12"  # 주식/ETF 호가
    
    
    class DBFI(QAxWidget):
        def __init__(self):
            super().__init__()
            self.id = "myid"  # HTS id
            self.pwd = "mypwd"  # HTS 비밀번호
            self.certpwd = "certpwd"  # 증권용 공인인증서 비밀번호
    
            self.setControl("DBFIOPENAPICOM.DBFIOpenAPIComCtrl.1")
    
            self.api_handle = -1
    
            # print("---- create api ------")
            hwnd = ctypes.windll.kernel32.GetModuleHandleA(None)  # 현재 윈도우 핸들 구하기
            # print("hwnd = {0}".format(hwnd))
    
            result = self.dynamicCall("CreateDongbuAPICtrl(str, int, int,)", self.id, 0,  hwnd)  # 로그인 윈도우를 실행한다.
            if result:
                print("--- 로그인 윈도우 실행 성공------")
            else:
                print("--- 로그인 윈도우 실행 실패.....------")
    
            self.stockcode = "005930"  # 삼성전자 주식코드 -- default 설정함
    
            self.Connected.connect(self._onconnected)
            self.Disconnected.connect(self._ondisconnected)
            self.ReceiveData.connect(self._receive_tr_data)
            self.ReceiveRTData.connect(self._receive_real_data)
    
        def login(self):
            result = self.dynamicCall("Login(str, str, str,  int)", self.id, self.pwd, self.certpwd, 1)  # 로그인 윈도우를 실행한다.
            return result
    
        def logout(self):
            result = self.dynamicCall("Logout()")
            return result
    
        def _onconnected(self, api_handle):
            print("connected...." + str(api_handle))
            self.api_handle = api_handle  # 인증받은 DongbuAPI Handle 저장
    
        def _ondisconnected(self):
            print("disconnected....")
    
        def _receive_tr_data(self, sender, data):
            print("=============== tr data ===================")
            print(type(sender), sender)
            print(type(data), len(data), data)
    
        def _receive_real_data(self, name, field, data):
            print("======== real data ===========")
            print(field)
            print(name)
            print(data)
    
        def get_login_info(self):
            print("----- info -----")
    
            # 주식 계좌 구하기
            bb = self.dynamicCall("GetAccountList(int)", 2)
            print("주식계좌 : ", bb)
    
            # 선물 계좌 구하기
            cc = self.dynamicCall("GetAccountList(int)", 1)
            print("선물계좌 : ", cc)
            print("---------------")
    
            result = self.dynamicCall("ReqStockHoga(str)", self.stockcode)
            if result:
                print("======== TR 요청 성공  ============")
    
        def get_real_data(self):
            result = self.dynamicCall("ReqRealtimeData(int, str, str)", ID_ADVICE_RT, R_X12, self.stockcode)
            return result
    
        def end_real_data(self):
            result = self.dynamicCall("ReqRealtimeData(int, str, str)", ID_UNADVICE_RT, R_X12, self.stockcode)
            return result
    
    
    if __name__ == "__main__":
        import sys
    
        class MyMain(QWidget):
            def __init__(self):
                super().__init__()
    
                self.dbfi = DBFI()
                self.dbfi.stockcode = "068270"  # 셀트리온 종목코드
    
                vbox = QVBoxLayout()
                self.qtxt = QTextEdit(self)
                vbox.addWidget(self.qtxt)
    
                hbox = QHBoxLayout()
                self._btn1 = QPushButton("Login", self)
                self._btn2 = QPushButton("Logout", self)
                self._btn3 = QPushButton("사용자정보, tr 요청", self)
                self._btn4 = QPushButton("real 요청", self)
                self._btn5 = QPushButton("real 중단", self)
    
                hbox.addWidget(self._btn1)
                hbox.addWidget(self._btn2)
                hbox.addWidget(self._btn3)
                hbox.addWidget(self._btn4)
                hbox.addWidget(self._btn5)
                vbox.addLayout(hbox)
                self.setLayout(vbox)
                self.setGeometry(300, 300, 300, 150)
    
                self._btn1.clicked.connect(self.btn1_clicked)
                self._btn2.clicked.connect(self.btn2_clicked)
                self._btn3.clicked.connect(self.__btn3_clicked)
                self._btn4.clicked.connect(self.__btn4_clicked)
                self._btn5.clicked.connect(self.__btn5_clicked)
    
                self._btn2.setEnabled(False)
                self._btn3.setEnabled(False)
                self._btn4.setEnabled(False)
                self._btn5.setEnabled(False)
    
            @pyqtSlot()
            def btn1_clicked(self):
                if self.dbfi.login():
                    self.qtxt.append("로그인 성공")
                    self._btn1.setEnabled(False)
                    self._btn2.setEnabled(True)
                    self._btn3.setEnabled(True)
                    self._btn4.setEnabled(True)
                    self._btn5.setEnabled(True)
                else:
                    self.qtxt.append("로그인 실패")
    
            @pyqtSlot()
            def btn2_clicked(self):
                if self.dbfi.logout():
                    self.qtxt.append("로그아웃 성공")
                else:
                    self.qtxt.append("로그아웃 실패")
    
            @pyqtSlot()
            def __btn3_clicked(self):
                self.dbfi.get_login_info()
    
            @pyqtSlot()
            def __btn4_clicked(self):
                if self.dbfi.get_real_data():
                    self.qtxt.append("실시간 요청 성공")
    
            @pyqtSlot()
            def __btn5_clicked(self):
                if self.dbfi.end_real_data():
                    self.qtxt.append("실시간 중단 요청 성공")
    
    
        app = QApplication(sys.argv)
        myWindow = MyMain()
        myWindow.show()
    
        app.exec_()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

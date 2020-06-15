---
title: kosdaq_data (1)
date: 2020-05-07
---
Example Python program kosdaq_data (1).py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from PyQt5.QtWidgets import *
* from PyQt5.QAxContainer import *
* from time import sleep

## Classes

* class Home(QMainWindow):

## Methods

* def __init__(self):
* def event_connect(self, err_code):
* def receive_trdata(self, screen_no, rqname, trcode, recordname, prev_next, data_len, err_code, msg1, msg2):
* def main():

## Code

Example Python PyQt program :

    import sys
    from PyQt5.QtWidgets import *
    from PyQt5.QAxContainer import *
    from time import sleep
    
    # 조회 제한: 1초당 5회
    
    class Home(QMainWindow):
        date = ""
        code = ""
    
        def __init__(self):
            super().__init__()
            self.setWindowTitle("PyStock")
    
            self.kiwoom = QAxWidget("KHOPENAPI.KHOpenAPICtrl.1")
            self.kiwoom.dynamicCall("CommConnect()")
    
            self.kiwoom.OnEventConnect.connect(self.event_connect)
            self.kiwoom.OnReceiveTrData.connect(self.receive_trdata)
    
        def event_connect(self, err_code):
            if err_code == 0:
                print("로그인 성공")
                # 출력=버전처리o
    
                with open("new_kosdaq_one_year.txt", "r") as data_file:
                    lines = data_file.readlines()
    
                for line in lines:
                    line = line.split()
                    self.code = line[0]
                    self.date = line[1]
    
                    print(self.code)
    
                    self.kiwoom.dynamicCall("SetInputValue(QString, QString)", "종목코드", self.code)
                    self.kiwoom.dynamicCall("SetInputValue(QString, QString)", "시작일자", self.date)
                    self.kiwoom.dynamicCall("SetInputValue(QString, QString)", "표시구분", "1")
                    self.kiwoom.dynamicCall("CommRqData(QString, QString, int, QString)", "opt10086_req", "opt10086", 0, "0101")
    
                    sleep(0.6)
    
        def receive_trdata(self, screen_no, rqname, trcode, recordname, prev_next, data_len, err_code, msg1, msg2):
    
            # 시가/고가/저가/종가/등락률/거래량/금액(백만)/개인/기관/외인수량/외국계/프로그램/외인비/체결강도/외인보유/외인순매수/기관순매수/개인순매수
            if rqname == "opt10086_req":
                data_list = ["시가", "고가", "저가", "종가", "등락률", "거래량", "금액(백만)", "개인", "기관", "외국계", "외인수량"
                    , "외인비", "프로그램", "체결강도", "외인보유", "외인순매수", "기관순매수", "개인순매수"]
    
                with open("new_kosdaq_kiwoom_data.txt", "a") as data_file:
                    data = self.code + " " + self.date + " "
                    for li in data_list:
                        tmp = self.kiwoom.dynamicCall("CommGetData(QString, QString, QString, int, QString)", trcode, "", rqname,
                                                   0, li)
                        data += tmp.strip() + " "
    
                    data_file.write(data.rstrip() + "\n")
    
    def main():
        app = QApplication(sys.argv)
        myWindow = Home()
        myWindow.show()
        app.exec_()
    
    if __name__ == "__main__":
        main()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

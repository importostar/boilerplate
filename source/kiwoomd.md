---
title: kiwoomd
date: 2020-05-07
---
Example Python program kiwoomd.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from PyQt5.QtWidgets import *
* from PyQt5.QAxContainer import *
* from PyQt5.QtCore import *
* import time
* import pandas as pd
* import sqlite3

## Classes

* class Kiwoom(QAxWidget):

## Methods

* def __init__(self):
* def _create_kiwoom_instance(self):
* def _set_signal_slots(self):
* def _comm_connect(self):
* def _event_connect(self,err_code):
* def _get_connect_state(self):
* def _receive_tr_data(self, sScrNo, sRQName, sTrCode, sRecordName, sPreNext, nDataLength, sErrorCode, sMessage,sSplmMsg):
* def _receive_real_data(self, sRealKey, sRealType, sRealData):
* def _receive_msg(self, sScrNo, sRQName, sTrCode, sMsg):
* def _receive_chejan_data(self, sGubun, nItemCnt, sFidList):
* def change_format(data):
* def _get_comm_data(self, strTrCode, strRecordName, nIndex, strItemName):
* def _comm_rq_data(self, sRQName, sTrCode, nPrevNext, sScreenNo):
* def _set_input_value(self, sID, sValue):
* def _get_repeat_cnt(self, sTrCode, sRecordName):
* def _get_comm_real_data(self,strRealType,nFid):
* def _get_login_info(self,sTag):
* def _send_order(self,sRQName,sScreenNo,sAccNo,nOrderType,sCode,nQty,nPrice,sHogaGb,sOrgOrderNo):
* def _get_chejan_data(self,nFid):
* def _set_real_reg(self, strScreenNo, strCodeList, strFidList, strRealType):
* def _set_real_remove(self,strScrNo,strDelCode):
* def _get_master_last_price(self,strCode):
* def _get_master_code_name(self,strCode):
* def _get_code_list_by_market(self,sMarket):
* def call_opw00001(self):
* def res_opw00001(self, strRecordName, strTrCode):
* def call_opw00011(self):
* def res_opw00011(self,strRecordName, strTrCode):
* def call_opw00018(self):
* def res_opw00018(self,strRecordName, strTrCode):
* def call_opt10001(self,sRealKey):
* def res_opt10001(self, strRecordName, strTrCode):
* def call_opt10085(self):
* def res_opt10085(self, strRecordName, strTrCode):
* def call_opt10004(self,sRealKey):
* def res_opt10004(self, strRecordName, strTrCode):
* def call_opt10081(self,sRealKey):
* def res_opt10081(self, strRecordName, strTrCode):
* def res_set_real2(self,ScrNo):
* def res_set_real3(self,ScrNo):
* def res_set_real4(self,ScrNo):

## Code

Example Python PyQt program :

    import sys
    from PyQt5.QtWidgets import *
    from PyQt5.QAxContainer import *
    from PyQt5.QtCore import *
    import time
    import pandas as pd
    import sqlite3
    
    
    
    
    class Kiwoom(QAxWidget):
        def __init__(self):
            super().__init__()
            self._create_kiwoom_instance()
            self._set_signal_slots()
        def _create_kiwoom_instance(self):
            self.setControl("KHOPENAPI.KHOpenAPICtrl.1")
        def _set_signal_slots(self):
            self.OnReceiveTrData.connect(self._receive_tr_data)
            self.OnReceiveRealData.connect(self._receive_real_data)
            self.OnReceiveMsg.connect(self._receive_msg)
            self.OnReceiveChejanData.connect(self._receive_chejan_data)
            self.OnEventConnect.connect(self._event_connect)
        def _comm_connect(self):
            self.dynamicCall("CommConnect()")
            self.login_event_loop=QEventLoop()
            self.login_event_loop.exec_()
        def _event_connect(self,err_code):
            if err_code==0:
                print("connected")
            else:
                print("disconnected")
            self.login_event_loop.exit()
        def _get_connect_state(self):
            ret=self.dynamicCall("GetConnectState()")
            return ret
    
    
    # 이벤트 처리하는곳
        def _receive_tr_data(self, sScrNo, sRQName, sTrCode, sRecordName, sPreNext, nDataLength, sErrorCode, sMessage,sSplmMsg):
            pass
        def _receive_real_data(self, sRealKey, sRealType, sRealData):
            pass
        def _receive_msg(self, sScrNo, sRQName, sTrCode, sMsg):
            pass
        def _receive_chejan_data(self, sGubun, nItemCnt, sFidList):
            pass
    # 이벤트 처리하는곳
    
    #기본함수 정의
        @staticmethod
        def change_format(data):
            strip_data = data.lstrip('-0')
            if strip_data == '':
                strip_data = '0'
    
            format_data = strip_data
            if data.startswith('-'):
                format_data = '-' + format_data
    
            return format_data
    
        def _get_comm_data(self, strTrCode, strRecordName, nIndex, strItemName):
            ret = self.dynamicCall("GetCommData(QString, QString, int, QString)", strTrCode,strRecordName, nIndex, strItemName)
            return ret.strip()
        def _comm_rq_data(self, sRQName, sTrCode, nPrevNext, sScreenNo):
            ret=self.dynamicCall("CommRqData(QString, QString, int, QString)", sRQName, sTrCode, nPrevNext, sScreenNo)
            return ret
        def _set_input_value(self, sID, sValue):
            self.dynamicCall("SetInputValue(QString, QString)", sID, sValue)
        def _get_repeat_cnt(self, sTrCode, sRecordName):
            ret = self.dynamicCall("GetRepeatCnt(QString, QString)", sTrCode, sRecordName)
            return ret
        def _get_comm_real_data(self,strRealType,nFid):
            ret=self.dynamicCall("GetCommRealData(QString,int)",strRealType,nFid)
            return ret.strip()
        def _get_login_info(self,sTag):
            ret=self.dynamicCall("GetLoginInfo(QString)",sTag)
            return ret
        def _send_order(self,sRQName,sScreenNo,sAccNo,nOrderType,sCode,nQty,nPrice,sHogaGb,sOrgOrderNo):
            ret=self.dynamicCall("SendOrder(QString, QString, QString, int, QString, int, int, QString, QString)", sRQName, sScreenNo, sAccNo, nOrderType, sCode, nQty, nPrice, sHogaGb, sOrgOrderNo)
            return ret
        def _get_chejan_data(self,nFid):
            ret=self.dynamicCall("GetChejanData(int)",nFid)
            return ret
        def _set_real_reg(self, strScreenNo, strCodeList, strFidList, strRealType):
            ret=self.dynamicCall("SetRealReg(QString,QString,QString,QString)", strScreenNo, strCodeList, strFidList,strRealType)
            return ret
        def _set_real_remove(self,strScrNo,strDelCode):
            ret=self.dynamicCall("SetRealRemove(QString,QString)",strScrNo,strDelCode)
            return ret
        def _get_master_last_price(self,strCode):
            ret=self.dynamicCall("GetMasterLastPrice(QString)",strCode)
            ret=Kiwoom.change_format(ret)
            return ret
        def _get_master_code_name(self,strCode):
            ret=self.dynamicCall("GetMasterCodeName(QString)",strCode)
            return ret
        def _get_code_list_by_market(self,sMarket):
            ret = self.dynamicCall("GetCodeListByMarket(QString)", sMarket)
            #0 장내 8 etf 10 코스닥
            return ret
    
    #기본함수 정의 끝
    
    
    
    #############       Tr 정의
        def call_opw00001(self):
            self._set_input_value("계좌번호","8091442811")
            self._set_input_value("비밀번호","0000")
            self._comm_rq_data("opw00001_req","opw00001",0,"2000")
        def res_opw00001(self, strRecordName, strTrCode):
            d2_deposit = self._get_comm_data(strTrCode, strRecordName, 0, "d+2추정예수금")
            self.d2_deposit = Kiwoom.change_format(d2_deposit)
            return self.d2_deposit
    
        def call_opw00011(self):
            self._set_input_value("계좌번호","8091442811")
            self._set_input_value("비밀번호", "")
            self._set_input_value("비밀번호입력매체구분", "00")
            self._set_input_value("종목번호", "039490")
            self._set_input_value("매수가격", "10000")
            self._comm_rq_data("opw00011_req", "opw00011", 0, "2001")
        def res_opw00011(self,strRecordName, strTrCode):
            posimoney=str(abs(int(self._get_comm_data(strTrCode, strRecordName, 0, "미수불가주문가능금액"))))
            self.posimoney=Kiwoom.change_format(posimoney)
            return self.posimoney
    
        def call_opw00018(self):
            self._set_input_value("계좌번호","8091442811")
            self._set_input_value("비밀번호", "")
            self._set_input_value("비밀번호입력매체구분", "00")
            self._set_input_value("조회구분", "1")
            self._comm_rq_data("opw00018_req", "opw00018", 0, "2002")
        def res_opw00018(self,strRecordName, strTrCode):
            buyasset=str(abs(int(self._get_comm_data(strTrCode, strRecordName, 0, "총매입금액"))))
            nowasset = str(abs(int(self._get_comm_data(strTrCode, strRecordName, 0, "총평가금액"))))
            if buyasset=="":
                buyasset=0
            if nowasset=="":
                nowasset=0
            self.buyasset=Kiwoom.change_format(buyasset)
            self.nowasset = Kiwoom.change_format(nowasset)
    
        def call_opt10001(self,sRealKey):
            self._set_input_value("종목코드",sRealKey)
            self._comm_rq_data("opt10001_req","opt10001",0,"2003")
        def res_opt10001(self, strRecordName, strTrCode):
            self.opt1=self._get_comm_data(strTrCode, strRecordName, 0, "자본금")
            self.opt2=self._get_comm_data(strTrCode, strRecordName, 0, "상장주식")
            self.opt3=self._get_comm_data(strTrCode, strRecordName, 0, "신융비율")
            self.opt4=self._get_comm_data(strTrCode, strRecordName, 0, "시가총액")
            self.opt5=self._get_comm_data(strTrCode, strRecordName, 0, "외인소진율")
            self.opt6=self._get_comm_data(strTrCode, strRecordName, 0, "PER")
            self.opt7=self._get_comm_data(strTrCode, strRecordName, 0, "ROE")
            self.opt8=self._get_comm_data(strTrCode, strRecordName, 0, "PBR")
            self.opt9=self._get_comm_data(strTrCode, strRecordName, 0, "EV")
            self.opt10=self._get_comm_data(strTrCode, strRecordName, 0, "BPS")
            self.opt11= self._get_comm_data(strTrCode, strRecordName, 0, "매출액")
            self.opt12=self._get_comm_data(strTrCode, strRecordName, 0, "영업이익")
            self.opt13=self._get_comm_data(strTrCode, strRecordName, 0, "당기순이익")
    
        def call_opt10085(self):
            self._set_input_value("계좌번호", "8091442811")
            self._comm_rq_data("opt10085_req","opt10085",0,"2004")
        def res_opt10085(self, strRecordName, strTrCode):
            self.opt85_1=[]
            self.opt85_2 = []
            self.opt85_3 = []
            self.opt85_4 = []
            self.opt85_r=self._get_repeat_cnt(strTrCode,strRecordName)
            for i in range(0,self.opt85_r):
                self.opt85_1.append(self._get_comm_data(strTrCode, strRecordName, i, "종목코드"))
                self.opt85_2.append(str(abs(int(self._get_comm_data(strTrCode, strRecordName, i, "매입가")))))
                self.opt85_3.append(str(abs(int(self._get_comm_data(strTrCode, strRecordName, i, "보유수량")))))
                self.opt85_4.append(str(abs(int(self._get_comm_data(strTrCode, strRecordName, i, "현재가")))))
    
        def call_opt10004(self,sRealKey):
            self._set_input_value("종목코드", sRealKey)
            self._comm_rq_data("opt10004_req", "opt10004", 0, "2005")
    
        def res_opt10004(self, strRecordName, strTrCode):
            self.opt04_1=self._get_comm_data(strTrCode,strRecordName,0,"매수최우선잔량")
            self.opt04_2=self._get_comm_data(strTrCode, strRecordName, 0, "매도최우선잔량")
    
        def call_opt10081(self,sRealKey):
            self._set_input_value("종목코드", sRealKey)
            self._set_input_value("기준일자", "20170807")
            self._set_input_value("수정주가구분", "0")
            self._comm_rq_data("opt10081_req", "opt10081", 0, "2006")
    
        def res_opt10081(self, strRecordName, strTrCode):
            self.opt81_r = self._get_repeat_cnt(strTrCode, strRecordName)
            self.opt81_1=[]
            self.opt81_2 = []
            self.opt81_3 = []
            self.opt81_4 = []
            self.opt81_5 = []
            self.opt81_6 = []
            for i in range(0,self.opt81_r):
                self.opt81_1.append(self._get_comm_data(strTrCode,strRecordName,i,"시가"))
                self.opt81_2.append(self._get_comm_data(strTrCode, strRecordName, i, "고가"))
                self.opt81_3.append(self._get_comm_data(strTrCode, strRecordName, i, "저가"))
                self.opt81_4.append(self._get_comm_data(strTrCode, strRecordName, i, "현재가"))
                self.opt81_5.append(self._get_comm_data(strTrCode, strRecordName, i, "거래량"))
                self.opt81_6.append(self._get_comm_data(strTrCode, strRecordName, i, "일자"))
    
    
        def res_set_real2(self,ScrNo):
            ret=self._set_real_reg(ScrNo, "015760;161890;161390;000240;047810;060980;008930;128940;009240;020000;105630;014680;004710;018880;009420;003300;051600;052690;097230;000880;088350;009830;012450;000720;005440;086280;267250;064350;079430;012330;010620;069960;012630;017800;011210;004020;009540;005380;001450;057050;008770;004800;093370;069260", "13;20;27;28;23;930;931;951;901;904;9203;911;910;9001", "1")
            return ret
        def res_set_real3(self,ScrNo):
            ret=self._set_real_reg(ScrNo, "006840;027410;138930;001040;079160;000120;097950;114090;078930;006360;007070;001060;096760;105560;002380;030200;033780;093050;003550;034220;001120;051900;032640;011070;066570;108670;051910;079550;006260;010120;035420;005940;010060;005490;064960;010950;034120;034730;011790;001740;096770;006120;017670;000660;005610;035250;000050;010130;002240;009290;011780;073240;000270;024110;003920;025860;002350;251270;006280;005250;004370;019680;008060;000210;001680;047040;069620;006650;003490;001230;000990;005830;026960;000640;170900;007340;001520;049770;014820;000150;042670;034020;115390;023530;004000;004990;005300;011170;002270;204320;008560;033920;006800;003850", "13;20;27;28;23;930;931;951;901;904;9203;911;910;9001", "1")
            return ret
        def res_set_real4(self,ScrNo):
            ret=self._set_real_reg(ScrNo, "003000;005180;006400;028260;207940;032830;018260;028050;009150;005930;010140;016360;029780;000810;145990;000070;004490;001430;003030;029530;004170;055550;003410;003620;002790;090430;010780;001780;005850;012750;078520;036570;111770;003520;000670;007310;271560;001800;000030;014830;000100;214320;139480;007570;020150;030000;002620;185750;192820;120110;021240;192400;003240;036580;028670;047050;103140;086790;000080;036460;071050;025540;002960", "13;20;27;28;23;930;931;951;901;904;9203;911;910;9001", "1")
            return ret

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

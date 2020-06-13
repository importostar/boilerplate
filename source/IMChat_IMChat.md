---
title: IMChat_IMChat
date: 2020-05-07
---
Example Python program IMChat_IMChat.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from  tkinter import *

## Methods

* def sendBtnClick(inputTextFied):
* def cleanBtnClick(inputTextFied):
* # def yscrollcommand():
* def init_IMCahtFrame():

## Code

Python tkinter example

    # encoding=utf8
    from  tkinter import *
    
    def sendBtnClick(inputTextFied):
        print('点击了发送')
        #GET的会有两个值 一个是获取的开始一个是结束
        text = inputTextFied.get(index1='1.0',index2='end')
        print(text)
    
    def cleanBtnClick(inputTextFied):
        print(inputTextFied.get())
    
    # def yscrollcommand():
    #     print('ceshi')
    
    def init_IMCahtFrame():
        # 聊天的主界面
        root = Tk()
        root.geometry('800x600')
        root.resizable(0, 0)
    
        # textArea = Text(root,width ='800',height='200',)
        # textArea.place(relx=0,rely=0.7)
        # 主窗口
        frame = Frame(root, width=800, height=600, bg='black')
        # 上窗口
        topFrame = Frame(frame, width=800, height=400, bg='blue')
        topLeftFrame = Frame(topFrame, width=200, height=400, bg="red")
        topRightFrame = Frame(topFrame, width=600, height=400, bg="black")
        topLeftTopFrame = Frame(topLeftFrame, width=200, height=150, bg='blue')
        topLeftDownFrame = Frame(topLeftFrame, width=200, height=250, bg='red')
        # 滚动条
        chatTextScrollbar = Scrollbar(topRightFrame)
        chatTextScrollbar.pack(side=RIGHT,fill=Y)#
        # 显示聊天文本
        chatText = Listbox(topRightFrame, width=64,height= 19,font=('微软雅黑', 11),yscrollcommand = chatTextScrollbar.set)
        for i in range(111):
            chatText.insert(END, i)
    
        chatText.pack(side=RIGHT,fill=Y)
        chatTextScrollbar.config(command = chatText.yview())
        # 位置
        frame.place(x=0, y=0)
        topFrame.place(x=0, y=0)
        topLeftFrame.place(x=0, y=0)
        topRightFrame.place(x=200, y=0)
        topLeftTopFrame.place(x=0, y=0)
        topLeftDownFrame.place(x=0, y=300)
    
        # 下窗口
        downFrame = Frame(frame, width=800, height=200, )
        downTextFrame = Frame(downFrame, width=800, height=150, bg='red')
        downBtnFrame = Frame(downFrame, width=800, height=50, bg='')
    
        # 下窗口的位置
        downFrame.place(x=0, y=401)
        downTextFrame.place(x=0, y=0)
        downBtnFrame.place(x=0, y=150)
    
        #输入消息的滚动条
        inputTextScroll = Scrollbar(downTextFrame)
        inputTextScroll.place(x=780,y=30)  #显示在右边 Farme.Y的距离pack(side=RIGHT,fill=Y)
        # 文本框
        inputTextFied = Text(downTextFrame, width=111, height=12,yscrollcommand = inputTextScroll.set)
        inputTextScroll.config(command = inputTextFied.yview())
        inputTextFied.place(x=0, y=0)
    
        # 按钮
        sendBtn = Button(downBtnFrame, text="Send", width=10, command=lambda:sendBtnClick(inputTextFied))
        cleanBtn = Button(downBtnFrame, text="Clean", width=10,command=lambda:cleanBtnClick(inputTextFied))
    
        # 按钮位置
        sendBtn.place(x=700, y=10)
        cleanBtn.place(x=600, y=10)
        #进入循环消息
        root.mainloop()
    
    
    if __name__ == '__main__':
        init_IMCahtFrame()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

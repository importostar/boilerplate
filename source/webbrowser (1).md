---
title: webbrowser (1)
date: 2020-05-07
---
Example Python program webbrowser (1).py

## Modules

* from tkinter import *
* import webbrowser

## Methods

* def google():
* def youtube():
* def amazon():
* def facebook():
* def gmail():
* def instagram():
* def twitter():
* def wikipedia():
* def flipkart():
* def netflix():
* def search():

## Code

Python tkinter example

    from tkinter import *
    import webbrowser
    
    win=Tk()
    win.title("Browser")
    win.geometry("320x250")
    win.iconbitmap('F:/pramod/tkinter/firefox.ico')
    win.config(background="sky blue")
    
    def google():
        webbrowser.open("https://www.google.com/")
        
    def youtube():
        webbrowser.open("https://www.youtube.com/")
    
    def amazon():
        webbrowser.open("https://www.amazon.in/")
    
    def facebook():
        webbrowser.open("https://www.facebook.com/")
        
    def gmail():
        webbrowser.open("https://www.gmail.com/")
    
    def instagram():
        webbrowser.open("https://www.instagram.com/")
    
    def twitter():
        webbrowser.open("https://twitter.com/explore")
    
    def wikipedia():
        webbrowser.open("https://www.wikipedia.org/")
    
    def flipkart():
        webbrowser.open("https://www.flipkart.com/")
    
    def netflix():
        webbrowser.open("https://www.netflix.com/in/")
    
    def search():
        url=e.get()
        webbrowser.open(url)
        
    igoogle=PhotoImage(file="F:/pramod/tkinter/webbrowser/google2.png")
    lbl=Label(win,text="Google",bg="sky blue").place(x=15,y=105)
    google=Button(win,image=igoogle,bg="sky blue",command=google)
    google.place(x=10,y=50)
    
    iyoutube=PhotoImage(file="F:/pramod/tkinter/webbrowser/youtube2.png")
    lbl1=Label(win,text="YouTube",bg="sky blue").place(x=70,y=105)
    youtube=Button(win,image=iyoutube,bg="sky blue",command=youtube)
    youtube.place(x=70,y=50)
    
    iamazon=PhotoImage(file="F:/pramod/tkinter/webbrowser/amazon.png")
    lbl5=Label(win,text="Amazon",bg="sky blue").place(x=10,y=185)
    amazon=Button(win,image=iamazon,bg="sky blue",command=amazon)
    amazon.place(x=10,y=130)
    
    ifacebook=PhotoImage(file="F:/pramod/tkinter/webbrowser/facebook.png")
    lbl6=Label(win,text="Facebook",bg="sky blue").place(x=70,y=185)
    facebook=Button(win,image=ifacebook,bg="sky blue",command=facebook)
    facebook.place(x=70,y=130)
    
    igmail=PhotoImage(file="F:/pramod/tkinter/webbrowser/gmail.png")
    lbl2=Label(win,text="Gmail",bg="sky blue").place(x=140,y=105)
    gmail=Button(win,image=igmail,bg="sky blue",command=gmail)
    gmail.place(x=130,y=50)
    
    iinstagram=PhotoImage(file="F:/pramod/tkinter/webbrowser/instagram2.png")
    lbl7=Label(win,text="Instagram",bg="sky blue").place(x=130,y=185)
    instagram=Button(win,image=iinstagram,bg="sky blue",command=instagram)
    instagram.place(x=130,y=130)
    
    itwitter=PhotoImage(file="F:/pramod/tkinter/webbrowser/twitter2.png")
    lbl=Label(win,text="Twitter",bg="sky blue").place(x=195,y=185)
    twitter=Button(win,image=itwitter,bg="sky blue",command=twitter)
    twitter.place(x=190,y=130)
    
    iwikipedia=PhotoImage(file="F:/pramod/tkinter/webbrowser/wikipedia.png")
    lbl3=Label(win,text="Wikipedia",bg="sky blue").place(x=190,y=105)
    wikipedia=Button(win,image=iwikipedia,bg="sky blue",command=wikipedia)
    wikipedia.place(x=190,y=50)
    
    iflipkart=PhotoImage(file="F:/pramod/tkinter/webbrowser/filpkart2.png")
    lbl=Label(win,text="Flipkart",bg="sky blue").place(x=255,y=185)
    flipkart=Button(win,image=iflipkart,bg="sky blue",command=flipkart)
    flipkart.place(x=250,y=130)
    
    inetflix=PhotoImage(file="F:/pramod/tkinter/webbrowser/netflix2.png")
    lbl4=Label(win,text="Netflix",bg="sky blue").place(x=255,y=105)
    netflix=Button(win,image=inetflix,bg="sky blue",command=netflix)
    netflix.place(x=250,y=50)
    
    e=Entry(win,width=20,font=('arial',10,'bold'))
    e.place(x=70,y=10)
    
    btn=Button(win,text="Search",font=('arial',10,'bold'),bg="blue",fg="white",bd=5,command=search)
    btn.place(x=216,y=5)
    
    win.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

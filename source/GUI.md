---
title: GUI
date: 2020-05-07
---
Example Python program GUI.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* #--------------------import modules---------------
* from tkinter import messagebox
* import tkinter
* import tweepy
* import time
* from tweepy.api import API
* from tweepy import Stream
* from tweepy import OAuthHandler
* from tweepy.streaming import StreamListener, json
* from textblob import TextBlob
* import matplotlib.pyplot as plt
* import numpy as np
* import _json
* import csv
* #from tkinter import *
* import os

## Methods

* def per(p, w):
* def comp():
* def analyzer():

## Code

Python tkinter example

    """ Aim: This code is used to fatch tweets using keyword. Analysis that tweet using textblob and sentiment. Convert result into pie chart. It also compare two person tweet and
             find who's tweet is more positive and nagetive and convert result into graph. csv file are used to store data.
        Ref:
              https://stackoverflow.com/questions/42559155/find-trending-tweets-with-tweepy-for-a-specific-keyword
              https://media.readthedocs.org/pdf/tweepy/latest/tweepy.pdf
              https://developer.twitter.com/en/docs/accounts-and-users/follow-search-get-users/api-reference/get-followers-ids
    """
    #--------------------import modules---------------
    from tkinter import messagebox
    
    import tkinter
    import tweepy
    import time
    from tweepy.api import API
    from tweepy import Stream
    from tweepy import OAuthHandler
    from tweepy.streaming import StreamListener, json
    from textblob import TextBlob
    import matplotlib.pyplot as plt
    import numpy as np
    import _json
    import csv
    
    #from tkinter import *
    import os
    
    #---------- define empty lists---------------
    x_axis = []
    y_axis = []
    id_list=[]
    tweet11=[]
    
    #---------- define percentage function ----------
    def per(p, w):
        return 100 * float(p) / float(w)
    
    #---------- define comparision function which compare two pwrson tweets----------
    
    def comp():
        global x_axis           # call global list
        global y_axis
        if os.path.isfile("modi_vs_trump.csv"):         #check file is there or not
         with open("modi_vs_trump.csv") as f:              #if there
            data = csv.reader(f, delimiter=' ')            #read data into csv file
            for r1 in data:
                temp = ",".join(r1)
               # print(temp)
                pola,subj=temp.split(",")               #split data when it find ,
                #print("type:",type(pola))
                pola1 = format(float(pola), '.2f')      # convert into two decimal floating point
                subj1 = format(float(subj), '.2f')
                x_axis.append(pola1)                    # append data into global list
                y_axis.append(subj1)
    
            #------------ ploting data into graph-----------
    
            print("x", x_axis)
            print("y", y_axis)
            plt.plot(x_axis, label="modi",color='orange')
            plt.plot(y_axis,label="trump",color='blue')
            plt.xlabel('polarity')
            plt.ylabel('subjectivity')
            plt.title('Line graph modi vs trump')
            plt.legend()
            plt.show()
        else:
            messagebox._show("error","NO file found")       #file not there show error messege pop up
    
    #------------- define function for serching keyword in all tweets------------
    
    def analyzer():
        #--------- secret key portion---------------
        API_KEY = 'dtVlycy0oLWVuUZu0XlnKi3Jn'
        API_SECRET = 'ycNRFfQ4CNQHz3ybqSVBg0iq0RAfyypqhDUkvsh6Pt3mBxDcfD'
        ACCESS_TOKEN = '985966341638115328-4LoymgCXxnPoQBFMhqzgdMjfQo6OvyY'
        ACCESS_TOKEN_SECRET = '6bP5E6XF8XyKtnL4tGi678NtQXIOVSTbPBdw54Jc2LCDu'
    
        #--------- connect client with twitter account-----------
    
        auth = tweepy.OAuthHandler(API_KEY, API_SECRET)
        auth.set_access_token(ACCESS_TOKEN, ACCESS_TOKEN_SECRET)
        api = tweepy.API(auth)
    
        #searchterm = input("enter keyword for search:")
        searchterm=name.get()
        no_Search1 = addr.get()
        if searchterm == "" and no_Search1=="":         #if data not enter then show error box
            messagebox.showinfo("No data found", "Check entered details")
            quit()
        else:
    
            modi_po=[]
            trump_po=[]
            no_Search=int(no_Search1)       #convert into integer
            trump_tweets = api.user_timeline(screen_name="realDonaldTrump", count=20)   # fatch 20 tweets of trump
            for t in trump_tweets:
    
                print(t.text)       #print its tweet
            modi_tweets=api.user_timeline(screen_name="narendramodi", count=20)         # fatch 20 tweet of modi
            for t1 in modi_tweets:
                modi_tweet=TextBlob(t1.text)            #anaylze modi tweet
    
                po,su=modi_tweet.sentiment              # find it polarity
                modi_po.append(po)                      # append polarity to list
            for t2 in trump_tweets:
                trump_tweet=TextBlob(t2.text)
                po1,su1=trump_tweet.sentiment
                trump_po.append(po1)
    
            #---------- write data into csv file----------------
    
            i=0
            while i<len(trump_po):                                  #continue until length of list
                with open("modi_vs_trump.csv", "a") as f:              #open file
                    no=modi_po[i]                                   # take 1st value from list
                    #print("no:",no)
                    no1=trump_po[i]
                    f.write(str(no))                            # write data into file
                    f.write(",")
                    f.write(str(no1))
                    f.write("\n")
                    f.close()
                    i+=1
            tweets = tweepy.Cursor(api.search, q=searchterm).items(no_Search)
    
            positive = 0
            negative = 0
            neutral = 0
            polarity = 0
    
            for tweet in tweets:
                all_data=TextBlob(tweet.text)       # analysis of tweets
               #print(tweet.text)
                global id_list,tweet11
                p,s=all_data.sentiment
            #--------------write data into file---------------
                with open("twitter_pol.csv","a") as f:
                    f.write(str(p))
                    f.write(",")
                    f.write(str(s))
                    f.write("\n")
                    f.close()
    
            #if s*100>0:
    
                #print("tweet exted:",tweet11.text)
                analysis= TextBlob(tweet.text)
                polarity+=analysis.sentiment.polarity
        #------------conut positivity negativity and neutral--------------
                if analysis.sentiment.polarity==0:
                    neutral+=1
                elif analysis.sentiment.polarity<0.00:
                    negative+=1
                elif analysis.sentiment.polarity>0.00:
                    positive+=1
            #print(tweet)
    
    #-----------find it's percentage value and convert into 2 decimal floating point-------------
    
            positive=per(positive,no_Search)
            positive = format(positive, '.2f')
            negative=per(negative,no_Search)
            negative = format(negative, '.2f')
            neutral=per(neutral,no_Search)
            neutral = format(neutral, '.2f')
    #----------ploting data into pie-chart---------------------
            labels=['positive['+str(positive)+'%]','neutral['+str(neutral)+'%]','negative['+str(negative)+'%]']
            sizes=[positive,neutral,negative]
            colors=["yellow","green","red"]
            patches,text=plt.pie(sizes, colors=colors)
            plt.legend(patches,labels,loc="best")
            plt.title("Analysis of tweeter tweet")
            plt.axis('equal')
            plt.show()
    #-----------GUI design--------------------
    root=tkinter.Tk()   #create new window
    root.config(bg="skyblue")
    
    root.title("TWEET ANALYZER")   #give title to window
    c2=tkinter.Canvas(width=590, height=350,bg="skyblue")
    label1=tkinter.Label(c2,text="enter world for tweet",font=(15))# create label
    label1.place(x=10,y=20) #place label
    label1.config(bg="skyblue")
    name=tkinter.Entry(root,bd=5)   #create entry box
    name.place(x=250,y=22)  #place it
    
    label2=tkinter.Label(c2,text="Number of tweets to analyze",font=(15))#create label
    label2.place(x=10,y=85)
    label2.config(bg="skyblue")
    addr=tkinter.Entry(c2,bd=5)
    addr.place(x=250,y=87)
    button1=tkinter.Button(c2,text="Random Word Analysis" ,command=analyzer)  #when save button cliked then savedata method called
    button2=tkinter.Button(c2,text="Modi VS Trump", command=comp)
    button1.place(x=140,y=190)
    button2.place(x=320,y=190)
    button1.config(bg="skyblue")
    button2.config(bg="skyblue")
    c2.pack()
    root.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

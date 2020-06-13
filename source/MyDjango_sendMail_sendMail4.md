---
title: MyDjango_sendMail_sendMail4
date: 2020-05-07
---
Example Python program MyDjango_sendMail_sendMail4.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import smtplib, time
* from email.mime.text import MIMEText
* from email.header import Header
* import threading
* import time

## Methods

* def profile(func):
* def wrapper(*args, **kwargs):
* def sendMail(times):
* def mainRun(times):
* def QueueSend(times):

## Code

Python example

    #!/usr/bin/python3
    
    import smtplib, time
    from email.mime.text import MIMEText
    from email.header import Header
    import threading
    
    semp = threading.Semaphore(3)
    
    
    def profile(func):
        def wrapper(*args, **kwargs):
            import time
            start = time.time()
            func(*args, **kwargs)
            end = time.time()
            print('COST: {}'.format(end - start))
    
        return wrapper
    
    
    def sendMail(times):
        # 第三方 SMTP 服务
        mail_host = "smtp.adbcedu.com.cn"  # 设置服务器
        mail_user = "wangb@adbcedu.com.cn"  # 用户名
        mail_pass = "asdf1234@"  # 口令
    
        sender = 'wangb@adbcedu.com.cn'
        receivers = ['admin@adbcedu.com.cn']  # 接收邮件，可设置为你的QQ邮箱或者其他邮箱
    
        message = MIMEText(
            'Python 邮件发送测试...Python 邮件发送测试...',
            'plain', 'utf-8')
        message['From'] = Header("菜鸟教程", 'utf-8')
        message['To'] = Header("测试", 'utf-8')
    
        subject = 'Python SMTP 邮件测试%s' % str(time.time())
        message['Subject'] = Header(subject, 'utf-8')
    
        try:
            smtpObj = smtplib.SMTP()
            smtpObj.connect(mail_host, 25)  # 25 为 SMTP 端口号
            smtpObj.login(mail_user, mail_pass)
            smtpObj.sendmail(sender, receivers, message.as_string())
            print("邮件发送成功:%d" % times)
        except smtplib.SMTPException:
            print("Error: 无法发送邮件%d!" % times)
    
    
    @profile
    def mainRun(times):
        threads = []
        for i in range(times):
            t = threading.Thread(target=sendMail, args=(i,))
            threads.append(t)
    
        for t in threads:
            t.setDaemon(True)
            t.start()
            main_thread = threading.currentThread()
            for t in threading.enumerate():
                if t is main_thread:
                    continue
                t.join()
    
                # t.join()
    
        print("Run Over! %s" % time.ctime())
    
    
    @profile
    def QueueSend(times):
        for i in range(times):
            sendMail(i)
    
    
    times = 100
    
    mainRun(times)
    # QueueSend(times)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

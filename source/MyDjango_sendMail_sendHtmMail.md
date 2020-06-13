---
title: MyDjango_sendMail_sendHtmMail
date: 2020-05-07
---
Example Python program MyDjango_sendMail_sendHtmMail.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import smtplib, time, threading
* from email.mime.text import MIMEText
* from email.header import Header

## Methods

* def sendMail(t):

## Code

Python example

    #!/usr/bin/python3
    
    import smtplib, time, threading
    from email.mime.text import MIMEText
    from email.header import Header
    
    
    def sendMail(t):
        # 第三方 SMTP 服务
        mail_host = "smtp.adbcedu.com.cn"  # 设置服务器
        mail_user = "wangb@adbcedu.com.cn"  # 用户名
        mail_pass = "qwer1234@"  # 口令
    
        sender = 'wangb@adbcedu.com.cn'
        receivers = ['postmaster@adbcedu.com.cn']  # 接收邮件，可设置为你的QQ邮箱或者其他邮箱
    
        # message = MIMEText(
        #     'Python 邮件发送测试...Python 邮件发送测试...Python 邮件发送测试...Python 邮件发送测试...Python 邮件发送测试...Python 邮件发送测试...Python 邮件发送测试...Python 邮件发送测试...Python 邮件发送测试...Python 邮件发送测试...Python 邮件发送测试...Python 邮件发送测试...Python 邮件发送测试...Python 邮件发送测试...Python 邮件发送测试...Python 邮件发送测试...Python 邮件发送测试...Python 邮件发送测试...Python 邮件发送测试...Python 邮件发送测试...Python 邮件发送测试...Python 邮件发送测试...Python 邮件发送测试...',
        #     'plain', 'utf-8')
        # message['From'] = Header("菜鸟教程", 'utf-8')
        # message['To'] = Header("测试", 'utf-8')
        #
        # subject = 'Python SMTP 邮件测试%s' % str(time.time())
        # message['Subject'] = Header(subject, 'utf-8')
    
        mail_msg = """
        <p>Python 邮件发送测试...</p>
        <p><a href="http://www.runoob.com">这是一个链接</a></p>
         <p><a href="http://www.runoob.com">这是一个链接</a></p>
          <p><a href="http://www.runoob.com">这是一个链接</a></p>
           <p><a href="http://www.runoob.com">这是一个链接</a></p>
            <p><a href="http://www.runoob.com">这是一个链接</a></p>
             <p><a href="http://www.runoob.com">这是一个链接</a></p> 
             <p><a href="http://www.runoob.com">这是一个链接</a></p>
              <p><a href="http://www.runoob.com">这是一个链接</a></p>
               <p><a href="http://www.runoob.com">这是一个链接</a></p>
                <p><a href="http://www.runoob.com">这是一个链接</a></p>
                 <p><a href="http://www.runoob.com">这是一个链接</a></p>
                  <p><a href="http://www.runoob.com">这是一个链接</a></p>
             
        """
        message = MIMEText(mail_msg, 'html', 'utf-8')
        message['From'] = Header("菜鸟教程", 'utf-8')
        message['To'] = Header("测试", 'utf-8')
    
        subject = 'Python SMTP 邮件测试%d' % t
        message['Subject'] = Header(subject, 'utf-8')
    
        try:
            smtpObj = smtplib.SMTP()
            smtpObj.connect(mail_host, 25)  # 25 为 SMTP 端口号
            smtpObj.login(mail_user, mail_pass)
            smtpObj.sendmail(sender, receivers, message.as_string())
            print("邮件发送成功:%d" % t)
        except smtplib.SMTPException:
            print("Error: 无法发送邮件")
    
    
    threads = []
    for i in range(10):
        # sendMail(i)
        # time.sleep(0.01)
        t = threading.Thread(target=sendMail, args=(i,))
        threads.append(t)
    
    for t in threads:
        t.setDaemon(True)
        t.start()
        #time.sleep(1)
    t.join()
    
    print("Run Over!")
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

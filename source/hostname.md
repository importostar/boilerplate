---
title: hostname
date: 2020-05-07
---
Example Python program hostname.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os
* from PyQt5 import QtCore, QtGui,  QtWidgets, uic
* from PyQt5.QtWidgets import QFileDialog, QTreeWidgetItem, QMessageBox
* import sys
* import paramiko
* import pysftp
* from libs.shh_thread import sshThread

## Classes

* class MyApp(QtWidgets.QWidget):

## Methods

* def __init__(self):
* def load_css(self):
* def event_handler(self):
* # def default_credentails(self):
* def connect_to_client(self):
* def verify_the_client(self):

## Code

Example Python PyQt program :

    import os
    from PyQt5 import QtCore, QtGui,  QtWidgets, uic
    from PyQt5.QtWidgets import QFileDialog, QTreeWidgetItem, QMessageBox
    import sys
    import paramiko
    import pysftp
    from libs.shh_thread import sshThread
    
    #paramiko.common.logging.basicConfig(level=paramiko.common.DEBUG)
    
    
    class MyApp(QtWidgets.QWidget):
    
        def __init__(self):
            super(MyApp, self).__init__()
            self.load_css()
            ui = os.path.join(os.path.dirname(__file__), './ui/hostname.ui')
            uic.loadUi(ui, self)
            self.event_handler()
            self.filename = 'change_hostname.sh'
    
    
        def load_css(self):
            cssFile = 'CSS/darkorange.stylesheet'
            with open(cssFile, 'r') as myfile:
                cssContent = myfile.read().replace('\n', '')
                app.setStyleSheet(cssContent)
    
        def event_handler(self):
            self.btn_set_hostname.clicked.connect(self.connect_to_client)
            self.btn_check_hostname.clicked.connect(self.verify_the_client)
    
        # def default_credentails(self):
        #     ip = self.te_ip_addr.toPlainText()
        #     computer_hostname = self.te_hostname.toPlainText()
        #     user = self.te_username.toPlainText()
        #     user_password = self.te_password.toPlainText()
    
        def connect_to_client(self):
            ipaddr = self.te_ip_addr.toPlainText()
            hostname = self.te_hostname.toPlainText()
            self.te_output.setText('connecting.... '+ str(ipaddr)
                                    +'\n hostname:' +hostname+' applied successfully')
    
            print('ip typed:'+ipaddr)
            print('hostname typed:'+hostname)
            ipaddr = self.te_ip_addr.toPlainText()
            ssh_username = self.te_username.toPlainText()
            ssh_password = self.te_password.toPlainText()
            #paramiko.util.log_to_file('./tmp/paramiko.log')
            remotepath = '/home/ubu-admin/' + self.filename
            localpath = './misc/' + self.filename
            cnopts = pysftp.CnOpts()
            cnopts.hostkeys = None
            with pysftp.Connection(host=ipaddr, username=ssh_username, password=ssh_password, cnopts=cnopts) as sftp:
                sftp.put(localpath, remotepath)
    
            # s = sftp.Connection
            #
            # s.put(localpath, remotepath)
            # s.close
    
            # ssh = paramiko.SSHClient()
            # ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
            # #ssh.load_host_keys(os.path.expanduser(os.path.join("~", ".ssh", "known_hosts")))
            # ssh.connect(ipaddr, username=ssh_username, password=ssh_password)
            # ftp_client = ssh.open_sftp()
            # print('copy file:'+localpath+'  '+'to this location:'+remotepath)
            # ftp_client.put(localpath, remotepath)
            # ftp_client.close()
            # ssh.close()
    
    
    
    
        def verify_the_client(self):
            hostname = self.te_hostname.toPlainText()
            ssh_username = self.te_username.toPlainText()
            ssh_password = self.te_password.toPlainText()
            ipaddr = self.te_ip_addr.toPlainText()
            ip_addr_lst = ipaddr.split(',')
    
            for i in range(len(ip_addr_lst)):
                self.ssh_job_threading = sshThread(i, ssh_username, ssh_password)
                print('==========')
                print(self.ssh_job_threading)
                print(self.ssh_job_threading)
    
                #self.ssh_job_threading.start()
    
    
    
    
    
            # ssh = paramiko.SSHClient()
            # ssh.load_system_host_keys()
            # ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
            # ssh.connect(ipaddr, username=ssh_username, password=ssh_password)
            # cmd = 'hostname'
            # print('command: ' + cmd)
            # ssh_stdin, ssh_stdout, ssh_stderr = ssh.exec_command(cmd)
            # ssh_stdout = ssh_stdout.readlines()
            # # ssh_stdout = ssh_stdout.read.splitlines()
            # print('output commandLine: ' + str(ssh_stdout))
            # print('output commandLine: ' + str(ssh_stdin))
            # print('output commandLine: ' + str(ssh_stderr))
            # output = str(ssh_stdout)
            # for line in output.replace(r'\n', '').replace(r"['",'').replace(r"']",'').split(','):
            #     print(line)
            #     self.te_output.setText('connecting.... ' + str(ipaddr)
            #                             + '\n current hostname: ' + str(line))
            # ssh.close()
    
    
    
    if __name__ == "__main__":
        app = QtWidgets.QApplication(sys.argv)
        window = MyApp()
        window.show()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

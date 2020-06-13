---
title: qt mailtray
date: 2020-05-07
---
Example Python program qt-mailtray.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5.QtWidgets import QApplication, QSystemTrayIcon, QMenu
* from PyQt5.QtGui import QIcon
* import sys
* import threading
* import os

## Classes

* class MailTray:

## Methods

* def __init__(self):
* def listen(self):
* def check_new(self, _=None):
* def state_idle(self, *args):
* def state_receiving(self, *args):
* def cleanup(self):

## Code

Example Python PyQt program :

    #!/usr/bin/python3
    
    # System tray icon displaying email syncing state.
    # Tell the tray that email is syncing:
    #   echo 'syncing' > $XDG_RUNTIME_DIR/mailtray.fifo
    # Sync has completed and recalculate new emails:
    #   echo 'idle' > $XDG_RUNTIME_DIR/mailtray.fifo
    #
    # Because in Qt, it's hard to use UNIX signals to tell the tray what's going on, we use a fifo to
    # inform the tray of the state.
    
    from PyQt5.QtWidgets import QApplication, QSystemTrayIcon, QMenu
    from PyQt5.QtGui import QIcon
    
    import sys
    import threading
    import os
    
    MAILDIR = os.environ.get('MAILDIR', os.path.expandvars("$HOME/Mail"))
    
    
    class MailTray:
        def __init__(self):
            self.app = QApplication([])
            self.app.setQuitOnLastWindowClosed(False)
            self.tray = QSystemTrayIcon()
    
            self.menu = QMenu()
            uc = self.menu.addAction('Update count')
            uc.triggered.connect(self.state_idle)
            quit = self.menu.addAction('Quit')
            quit.triggered.connect(self.cleanup)
            self.tray.setContextMenu(self.menu)
    
            self.icon_clean = QIcon.fromTheme('mail_generic')
            self.icon_new = QIcon.fromTheme('mail_new')
            self.icon_recieve = QIcon.fromTheme('mail-send-receive')
    
            self.new_count = {}
            self.state_idle()
            self.tray.setVisible(True)
    
            try:
                self.fifofile = os.path.join(os.environ['XDG_RUNTIME_DIR'], 'mailtray.fifo')
            except KeyError:
                print('XDG_RUNTIME_DIR is not set')
                sys.exit(1)
            try:
                os.mkfifo(self.fifofile)
            except FileExistsError:
                pass
    
            self.thread = threading.Thread(target=self.listen, daemon=True)
            self.thread.start()
    
        def listen(self):
            while True:
                with open(self.fifofile) as f:
                    line = f.readline().strip()
                    if line == 'syncing':
                        self.state_receiving()
                    elif line == 'idle':
                        self.state_idle()
                    elif line == 'exit':
                        self.cleanup()
    
        def check_new(self, _=None):
            self.new_count = {
                acc: len(list(filter(bool, os.popen(
                    f"""sh -c 'find "{MAILDIR}/{acc}/Inbox/new/" -type f -print0'"""
                ).read().split('\0'))))
                for acc in filter(lambda s: not s.startswith('.'), os.listdir(MAILDIR))
            }
    
        def state_idle(self, *args):
            self.check_new()
            msg = ', '.join(f'{a} ({n})'
                            for a, n in filter(lambda it: it[1] != 0, self.new_count.items()))
            if msg:
                self.tray.setToolTip(msg)
                self.tray.setIcon(self.icon_new)
            else:
                self.tray.setToolTip('Mail')
                self.tray.setIcon(self.icon_clean)
    
        def state_receiving(self, *args):
            self.tray.setToolTip('Syncing')
            self.tray.setIcon(self.icon_recieve)
    
        def cleanup(self):
            try:
                os.remove(self.fifofile)
            except Exception:
                pass
            self.app.quit()
    
    
    if __name__ == '__main__':
        os.environ['QT_LOGGING_RULES'] = 'qt5ct.debug=false'
        mailtray = MailTray()
        mailtray.app.exec_()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

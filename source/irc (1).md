---
title: irc (1)
date: 2020-05-07
---
Example Python program irc (1).py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import asyncio
* import ssl
* import signal
* from random import choice
* from logging import basicConfig
* from logging import getLogger
* from PyQt5 import QtWidgets, uic
* from quamash import QEventLoop
* import asyncio
* import ssl
* import signal
* from PyIRC.signal import event
* from PyIRC.line import Line
* from PyIRC.io.asyncio import IRCProtocol
* from PyIRC.extensions import bot_recommended

## Classes

* class MainWindow(QtWidgets.QMainWindow, formClass):
* class TestProtocol(IRCProtocol):

## Methods

* def __init__(self):
* def disconnect(self):
* def close(self):
* def connect(self):
* def sigint(*protos):
* def data_received(self, data):
* def respond(self, event, line):

## Code

Example Python PyQt program :

    #!/usr/bin/env python3.5
    
    import sys
    import asyncio
    import ssl
    import signal
    from random import choice
    from logging import basicConfig
    
    # ?
    from logging import getLogger
    _logger = getLogger(__name__)  # pylint: disable=invalid-name
    
    # PyQt5
    from PyQt5 import QtWidgets, uic
    from quamash import QEventLoop
    
    import asyncio
    import ssl
    import signal
    
    # PyIRC
    from PyIRC.signal import event
    from PyIRC.line import Line
    from PyIRC.io.asyncio import IRCProtocol
    from PyIRC.extensions import bot_recommended
    
    formClass = uic.loadUiType('main.ui')[0]
    
    class MainWindow(QtWidgets.QMainWindow, formClass):
    
        def __init__(self):
            super(MainWindow, self).__init__()
            self.setupUi(self)
            self.actionConnect.triggered.connect(self.connect)
            self.actionDisconnect.triggered.connect(self.disconnect)
            self.actionExit_2.triggered.connect(self.close)
            self.mainStatus.setPlainText('teste')
    
            self._server = None
            self._task = None
            self._server_running = None
    
        def disconnect(self):
            if self._server_running:
                try:
                    self._server.send("QUIT", ["Bye!"])
                    self._server.close()
                    self._task.cancel()
                except Exception as e:
                    print(e)
                finally:
                    self._server_running = False
                    self._server = None
                    self._Task = None
    
        def close(self):
            self.disconnect()
            return super().close()
    
        def connect(self):
    
            basicConfig(level="DEBUG")
    
            # @todo: place it in a file / preference window
            args = {
                'serverport': ('irc.freenode.net', 6667),
                'ssl': False,
                'username': 'jpbot',
                'nick': 'jpbot',
                'gecos': 'hello everybody',
                'extensions': bot_recommended,
                'join': ['#bot7'],
            }
    
            def sigint(*protos):
                for proto in protos:
                    try:
                        proto.send("QUIT", ["Terminating due to ctrl-c!"])
                        proto.close()
                    except Exception as e:
                        # Ugh! A race probably happened. Yay, signals.
                        pass
    
                print()
                print("Terminating due to ctrl-c!")
    
                quit()
    
            # IRC connect
            self._server = TestProtocol(**args)
            self._task = asyncio.ensure_future(self._server.connect())
            self._server_running = True
    
    class TestProtocol(IRCProtocol):
    
        yifflines = (
            "right there~",
            "mmmm yes~",
        )
    
        flirtlines = (
            "not in here! message me",
            "I don't do it in channels, sorry...",
        )
    
        def data_received(self, data):
            data = self.data + data
    
            lines = data.split(b'\r\n')
            self.data = lines.pop()
    
            for line in lines:
                line = Line.parse(line.decode('utf-8', 'ignore'))
                _logger.debug("IN: %s", str(line).rstrip())
                try:
                    super().recv(line)
                except Exception:
                    # We should never get here!
                    _logger.exception("Exception received in recv loop")
                    self.send("QUIT", ["Exception received!"])
                    self.transport.close()
    
                    # This is fatal and needs to be reported so stop the event
                    # loop.
                    loop = asyncio.get_event_loop()
                    loop.stop()
    
                    raise
    
        @event("commands", "PRIVMSG")
        def respond(self, event, line):
            print(dir(self.basic_rfc))
            params = line.params
    
            if len(params) < 2:
                return
    
            if self.casecmp(self.basic_rfc.nick, params[0]):
                params = [line.hostmask.nick, choice(self.yifflines)]
            else:
                # Ensure it starts with us
                check_self = params[-1][:len(self.basic_rfc.nick)]
                if not self.casecmp(self.basic_rfc.nick, check_self):
                    return
    
                params = [params[0], choice(self.flirtlines)]
    
            self.send("PRIVMSG", params)
    
    app = QtWidgets.QApplication(sys.argv)
    loop = QEventLoop(app)
    asyncio.set_event_loop(loop)
    
    if __name__ == '__main__':
        # initialize window
        window = MainWindow()
        window.show()
        sys.exit(app.exec_())
    
        try:
            loop.run_forever()
        finally:
            loop.close()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: async_slot2
date: 2020-05-07
---
Example Python program async_slot2.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import math
* import sys
* import asyncio
* from functools import partial
* from PyQt5.QtWidgets import QApplication, QWidget, QPushButton, QGridLayout, QProgressBar
* from PyQt5.QtNetwork import QNetworkAccessManager, QNetworkRequest
* from PyQt5.QtCore import QUrl
* from quamash import QEventLoop

## Classes

* class MyWidget(QWidget):

## Methods

* def async_reply(reply, signal='finished'):
* def __init__(self, parent=None):
* def on_test(self):
* async def _on_test(self):
* def on_click(self, i):
* async def _on_click(self, i):
* def main():

## Code

Example Python PyQt program :

    import math
    import sys
    import asyncio
    from functools import partial
    
    from PyQt5.QtWidgets import QApplication, QWidget, QPushButton, QGridLayout, QProgressBar
    from PyQt5.QtNetwork import QNetworkAccessManager, QNetworkRequest
    from PyQt5.QtCore import QUrl
    
    from quamash import QEventLoop
    
    
    def async_reply(reply, signal='finished'):
        future = asyncio.Future()
        getattr(reply, signal).connect(lambda: future.set_result(None))
        return future
    
    class MyWidget(QWidget):
    
        def __init__(self, parent=None):
            super().__init__(parent)
            layout = QGridLayout()
            self.nam = QNetworkAccessManager()
    
            self.pairs = []
            for i in range(10):
                b = QPushButton('Countdown: &%d' % i, clicked=partial(self.on_click, i))
                p = QProgressBar(visible=False)
                layout.addWidget(b, i, 0)
                layout.addWidget(p, i, 1)
                self.pairs.append((b, p))
    
            self.test_button = QPushButton('&test', clicked=self.on_test)
            layout.addWidget(self.test_button, i, 0)
    
            self.setLayout(layout)
    
        def on_test(self):
            asyncio.ensure_future(self._on_test())
    
        async def _on_test(self):
            self.test_button.setEnabled(False)
            print('getting')
            for i in range(30):
                await asyncio.sleep(.1)
                print('.', end='', flush=True)
    
            req = QNetworkRequest(QUrl('https://www.google.com'))
            reply = self.nam.get(req)
            await async_reply(reply)
            print('got', len(reply.readAll()), 'bytes')
            self.test_button.setEnabled(True)
    
        def on_click(self, i):
            asyncio.ensure_future(self._on_click(i))
    
        async def _on_click(self, i):
            b, p = self.pairs[i]
            b.setEnabled(False)
            p.setVisible(True)
    
            n = i * 100
            p.setMaximum(n)
    
            while n >= 0:
    
                await asyncio.sleep(0.01)
    
                p.setValue(n)
                b.setText('Countdown: %d' % math.ceil(n / 100))
                n -= 1
    
            b.setText('Countdown: &%d' % i)
            b.setEnabled(True)
            p.setVisible(False)
    
    
    def main():
        app = QApplication(sys.argv)
        loop = QEventLoop(app)
        asyncio.set_event_loop(loop)  # NEW must set the event loop
    
        w = MyWidget()
        w.show()
    
        with loop:
            loop.run_forever()
    
    if __name__ == '__main__':
        main()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

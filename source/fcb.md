---
title: fcb
date: 2020-05-07
---
Example Python program fcb.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import logging
* import sys
* import time
* import rtmidi
* import liblo
* from rtmidi.midiutil import open_midiinput, open_midioutput
* from PyQt5.QtWidgets import QWidget, QApplication
* from PyQt5.QtGui import QPainter, QColor, QFont
* from PyQt5.QtCore import Qt, QPointF, QRectF, QTimer, pyqtSlot, pyqtSignal

## Classes

* class SetlistApp(QWidget):

## Methods

* def drawText(qp, x, y, flags, text, boundingRect = 0):
* def drawText2(qp, point, flags, text, boundingRect = 0):
* def __init__(self):
* def saySomething(self, str):
* def change_song(self, path, args):
* def change_status(self, message):
* def tick(self):
* def initUI(self):
* def paintEvent(self, event):
* def drawText(self, event, qp):
* def drawShapes(self, qp):
* def closeEvent(self, event):

## Code

Example Python PyQt program :

    import logging
    import sys
    import time
    import rtmidi
    import liblo
    from rtmidi.midiutil import open_midiinput, open_midioutput
    from PyQt5.QtWidgets import QWidget, QApplication
    from PyQt5.QtGui import QPainter, QColor, QFont
    from PyQt5.QtCore import Qt, QPointF, QRectF, QTimer, pyqtSlot, pyqtSignal
    
    #except KeyboardInterrupt:
    #    print('')
    #finally:
    
    def drawText(qp, x, y, flags, text, boundingRect = 0):
        size = 32767.0
        corner = QPointF(x, y - size)
        if flags & Qt.AlignHCenter:
            corner.setX(corner.x() - size/2.0)
        elif flags & Qt.AlignRight:
            corner.setX(corner.x() - size)
        if flags & Qt.AlignVCenter:
            corner.setY(corner.y() + size/2.0)
        elif flags & Qt.AlignTop:
            corner.setY(corner.y() + size)
        else:
            flags = flags | Qt.AlignBottom
    
        rect = QRectF(corner.x(), corner.y(), size, size);
        qp.drawText(rect, flags, text);
    
    # http://stackoverflow.com/a/24831796/2393963
    # thank god for this
    def drawText2(qp, point, flags, text, boundingRect = 0):
        drawText(qp, point.x(), point.y(), flags, text, boundingRect);
    
    class SetlistApp(QWidget):
        trigger = pyqtSignal(str)
    
        def __init__(self):
            super().__init__()
    
            #self.log = logging.getLogger('midiin_poll')
            #logging.basicConfig(level=logging.DEBUG)
    
            #self.port = sys.argv[1] if len(sys.argv) > 1 else None
    
            try:
                # Change to none if not detected!!!
                self.midiin, self.in_port_name = open_midiinput(0)
            except (EOFError, KeyboardInterrupt):
                sys.exit()
    
            try:
                self.from_max = liblo.Server(7405)
                self.to_max = liblo.Address(7407)
            except liblo.ServerError as err:
                print(err)
                sys.exit()
    
            self.from_max.add_method("/song", 'i', self.change_song)
    
            self.song_idx = 0
            self.midiout = rtmidi.MidiOut()
            self.available_ports = self.midiout.get_ports()
            self.midiout.open_virtual_port("Virtual FCB")
            self.status = False
            self.actions = ['M', 'L', 'LI', 'M', 'M',
                    'L', 'L', 'L', 'LI', 'L']
            self.actions = self.actions[5:] + self.actions[:5]
            self.states = [False] * 10
            self.songs = [
                          ("Vale", 0),
                          ("Vem por dentro", 11),
                          ("Paralisia", 2),
                          ("Tava", 4),
                          ("Baú", 5),
                          ("My City", 6),
                          ("Turbulência", 10),
                          ("Almoço", 9),
                          ("Cabosse", 7),
                          ("Lascado", 8),
                          ("Escorbuto", 1)
                          ]
            self.lightGray = QColor(230, 230, 230)
            self.halfGray = QColor(211, 211, 211)
            self.darkGray = QColor(51, 51, 51)
            self.greenBlue = QColor(0, 255, 194)
    
            self.trigger.connect(self.saySomething)
    
            self.timer = QTimer()
            self.timer.timeout.connect(self.tick)
            self.timer.start(10)
            self.initUI()
    
        @pyqtSlot(str)
        def saySomething(self, str):
            pass
            #print("hmm")
    
        def change_song(self, path, args):
            i = args[0]
            if path == "/song":
                self.song_idx = min(max(0, self.song_idx + i), len(self.songs) - 1)
                print(self.song_idx)
                liblo.send(self.to_max, "/song", self.songs[self.song_idx][1])
            self.update()
    
    
        def change_status(self, message):
            # 176 (cc at channel 0)
            # 20-31 is undefined for MIDI
            # notes from 61 to 71
            CC_AT_CH0 = 183
            val = message[1] - 41
            idx = message[1] - 61
    
            final_msg = []
            if message[0] == 146:
                if self.actions[idx] == 'L':
                    if message[2] == 100:
                        self.states[idx] = not self.states[idx]
                        final_msg = [CC_AT_CH0, val, 0 if self.states[idx] == False else 127]
                        self.midiout.send_message(final_msg)
                        self.trigger.emit("opa")
                if self.actions[idx] == 'LI':
                    if message[2] == 100:
                        final_msg = [CC_AT_CH0, val, 0 if self.states[idx] == False else 127]
                        self.states[idx] = not self.states[idx]
                        self.midiout.send_message(final_msg)
                        self.trigger.emit("opa")
                elif self.actions[idx] == 'A':
                    if message[2] != 0:
                        final_msg = [CC_AT_CH0, val, 127]
                        self.midiout.send_message(final_msg)
                        self.states[idx] = True
                elif self.actions[idx] == 'M':
                    final_msg = [CC_AT_CH0, val, 0 if message[2] == 0 else 127]
                    self.midiout.send_message(final_msg)
                    self.states[idx] = False if message[2] == 0 else True
            if final_msg:
                print(final_msg)
                print("---")
            self.update()
    
    
        def tick(self):
            self.from_max.recv(0)
            msg = self.midiin.get_message()
    
            if msg:
                message, deltatime = msg
                #print("[%s] @%0.6f %r" % (in_port_name, timer, message))
    
                self.change_status(message)
    
    
        def initUI(self):
            self.setGeometry(300, 300, 280, 170)
            self.setWindowTitle("Setlist")
            #self.show()
            p = self.palette()
            p.setColor(self.backgroundRole(), Qt.white)
            self.setPalette(p)
            #self.showFullScreen()
            self.show()
    
        def paintEvent(self, event):
            qp = QPainter()
            qp.begin(self)
            qp.setRenderHint(QPainter.Antialiasing)
            self.drawShapes(qp)
            self.drawText(event, qp)
            qp.end()
    
        def drawText(self, event, qp):
            qp.setPen(self.darkGray)
            qp.setFont(QFont("Baskerville", 50))
    
            for idx, song in enumerate(self.songs):
                qp.setPen(self.darkGray)
                drawText2(qp,
                        QPointF(90, 70 + (idx * 73)),
                        Qt.AlignVCenter,
                        song[0],
                        boundingRect=0)
    
            qp.setPen(Qt.NoPen)
            qp.setBrush(self.greenBlue)
            qp.drawEllipse(QPointF(60, 70 + (self.song_idx * 73)), 20, 20)
    
            qp.setPen(self.darkGray)
            qp.setFont(QFont("Karla", 30))
            qp.drawText(QPointF(549, 338), "FILTER")
            qp.drawText(QPointF(687, 338), "FUZZ")
            qp.drawText(QPointF(828, 338), "SLAP")
            qp.drawText(QPointF(955, 338), "DELAY")
            qp.drawText(QPointF(600, 182), "VIBRATO")
            qp.drawText(QPointF(750, 182), "BOOST")
            qp.drawText(QPointF(850, 182), "VERB")
    
        def drawShapes(self, qp):
            qp.setPen(Qt.NoPen)
            qp.drawEllipse(QPointF(55, 400), 15, 15)
            qp.setBrush(self.lightGray)
            qp.drawRect(527, 0, 753, 347)
    
            for idx, x in enumerate(range(630, 1280, 136)):
                qp.setBrush(self.darkGray)
                qp.drawRect(x, 50, 60, 125)
                if self.states[idx + 5]:
                    qp.setBrush(self.greenBlue)
                    qp.drawEllipse(QPointF(x + 30, 113), 20, 20)
    
            for idx, x in enumerate(range(560, 1180, 136)):
                qp.setBrush(self.darkGray)
                qp.drawRect(x, 209, 60, 125)
                if self.states[idx]:
                    qp.setBrush(self.greenBlue)
                    qp.drawEllipse(QPointF(x + 30, 272), 20, 20)
    
            #if self.states[0]:
            #    qp.setBrush(self.greenBlue)
            #    qp.drawEllipse(QPointF(55, 400), 50, 50)
    
            qp.setBrush(self.halfGray)
            qp.drawRect(527, 28, 753, 14)
            qp.drawRect(527, 153, 753, 38)
            qp.drawRect(527, 309, 753, 38)
    
        def closeEvent(self, event):
            self.midiin.close_port()
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        ex = SetlistApp()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

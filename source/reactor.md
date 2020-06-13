---
title: reactor
date: 2020-05-07
---
Example Python program reactor.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import socket
* import time
* import selectors

## Classes

* class Poller:
* class Channel:
* class EventLoop:
* class Acceptor:
* class TcpConnection:

## Methods

* def __init__(self, eventloop):
* def poll(self, timeoutMs, channels):
* def updateChannel(self, channel):
* def removeChannel(self, channel):
* def __init__(self, s, eventloop):
* def events(self):
* def setEvents(self, events):
* def fd(self):
* def setReadCallback(self, cb):
* def setWriteCallback(self, cb):
* def setErrorCallback(self, cb):
* def enableRead(self):
* def enableWrite(self):
* def disableRead(self):
* def disableAll(self):
* def handleEvent(self, timeStamp):
* def __init__(self):
* def loop(self):
* def updateChannel(self, channel):
* def __init__(self, loop, ip = "127.0.0.1", port = 1234):
* def onNewConnection(self, s, timeStamp):
* def onWriteCallback(self, s, timeStamp):
* def onErrorCallback(self, s, timeStamp):
* def __init__(self, s):

## Code

Python example

    import socket
    import time
    import selectors
    
    kReadEvent  = selectors.EVENT_READ
    kWriteEvent = selectors.EVENT_WRITE
    kNoneEvent  = 0
    
    class Poller:
        """ I/O 多路分发
        """
    
        sel = None
        channels = {}
        eventLoop = None
    
        def __init__(self, eventloop):
            self.eventLoop = eventloop
            self.sel = selectors.DefaultSelector()
    
        def poll(self, timeoutMs, channels):
            assert isinstance(channels, list)
    
            ret = self.sel.select(timeoutMs)
            for (key, e) in ret:
                assert key.fd in self.channels
                if key.fd not in self.channels:
                    print("发现一个不存在的socket!\n")
                    print(self.channels)
                    return
    
                channel = self.channels[key.fd]
                channel.setEvents(e)
                channels.append(self.channels[key.fd])
    
        def updateChannel(self, channel):
            assert isinstance(channel, Channel)
    
            fd = channel.fd()
            events = channel.events()
            self.sel.register(fd, events)
    
            if fd not in self.channels: self.channels[fd] = channel
    
        def removeChannel(self, channel):
            assert isinstance(channel, Channel)
    
            fd = channel.fd()
            assert fd in self.channels
            self.sel.unregister(fd)
            del self.channels[fd]
    
    class Channel:
    
        s         = None   # socket
        event    = kNoneEvent   # 当前触发的事件
        eventLoop = None
    
        readCallback = None
        writeCallback = None
        errorCallback = None
    
        def __init__(self, s, eventloop):
            self.s = s
            self.eventLoop = eventloop
            pass
    
        def events(self):
            return self.event
    
        def setEvents(self, events):
            self.event = events
    
        def fd(self):
            return self.s.fileno()
    
        def setReadCallback(self, cb):
            self.readCallback = cb
    
        def setWriteCallback(self, cb):
            self.writeCallback = cb
    
        def setErrorCallback(self, cb):
            self.errorCallback = cb
    
        def enableRead(self):
            self.event |= kReadEvent
    
        def enableWrite(self):
            self.event |= kWriteEvent
    
        def disableRead(self):
            self.event &= ~kReadEvent
    
        def disableAll(self):
            self.event = kNoneEvent
    
        def handleEvent(self, timeStamp):
            if self.event & kReadEvent and self.readCallback:
                self.readCallback(self.fd(), timeStamp)
            elif self.event & kWriteEvent and self.writeCallback:
                self.writeCallback(self.fd(), timeStamp)
            else:
                self.errorCallback(self.fd(), timeStamp)
    
    class EventLoop:
    
        quit = False
        poller = None
    
        def __init__(self):
            self.poller = Poller(self)
    
        def loop(self):
            assert self.poller
            activeChannels = []
            while not self.quit:
                self.poller.poll(None, activeChannels)
                now = int(time.time())
                for channel in activeChannels:
                    channel.handleEvent(now)
    
        def updateChannel(self, channel):
            self.poller.updateChannel(channel)
    
    class Acceptor:
    
        ip   = None
        port = None
        sock = None
        channel = None
        eventloop = None
    
        def __init__(self, loop, ip = "127.0.0.1", port = 1234):
            self.eventloop = loop
    
            self.sock = socket.socket()
            self.sock.bind((ip, port))
            self.sock.setblocking(False)
            self.sock.setsockopt(socket.SOL_IP, socket.SO_REUSEADDR, True)
            self.sock.listen()
    
            self.channel = Channel(self.sock, self.eventloop)
            self.channel.setReadCallback(self.onNewConnection)
            self.channel.setWriteCallback(self.onWriteCallback)
            self.channel.setErrorCallback(self.onErrorCallback)
            self.channel.enableRead()
    
            self.eventloop.updateChannel(self.channel)
    
        def onNewConnection(self, s, timeStamp):
            assert s == self.sock.fileno()
            (new_socket, addr) = self.sock.accept()
            new_socket.send(b"hello")
            new_socket.close()
            pass
    
        def onWriteCallback(self, s, timeStamp):
            pass
    
        def onErrorCallback(self, s, timeStamp):
            pass
    
    class TcpConnection:
    
        def __init__(self, s):
            pass
    
    if __name__ == '__main__':
        loop = EventLoop()
        acceptor = Acceptor(loop)
    
        loop.loop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: perf
date: 2020-05-07
---
Example Python program perf.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from socket import *
* from threading import Thread
* import time

## Methods

* def monitor():

## Code

Python example

    from socket import *
    from threading import Thread
    import time
    
    sock = socket(AF_INET, SOCK_STREAM)
    sock.connect(("localhost", 5000))
    
    n = 0
    
    
    def monitor():
        global n
        while True:
            time.sleep(1)
            print(n, 'req/sec')
            n = 0
    
    
    Thread(target=monitor).start()
    
    while True:
        sock.send(b'1')
        resp = sock.recv(100)
        n += 1
    
    # Example: running perf2 program and passing "big" number to our fib server
    # 21717 req/sec
    # 25164 req/sec
    # 24865 req/sec
    # 25188 req/sec
    # 6954 req/sec <- we notice that GIL prioritize CPU extensive task and that affects our requests
    # 148 req/sec  <- it has to do with internal implementation of GIL itself and it's not how OS do things
    # 147 req/sec
    # 145 req/sec
    # 148 req/sec
    # 140 req/sec
    # 146 req/sec
    # 144 req/sec
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: fib_server_treads_pool
date: 2020-05-07
---
Example Python program fib_server_treads_pool.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from socket import *
* from fib import fib
* from threading import Thread
* from concurrent.futures import ProcessPoolExecutor as Pool

## Methods

* def fib_server(address):
* def fib_handler(client):

## Code

Python example

    from socket import *
    from fib import fib
    from threading import Thread
    from concurrent.futures import ProcessPoolExecutor as Pool
    
    
    def fib_server(address):
        sock = socket(AF_INET, SOCK_STREAM)
        sock.setsockopt(SOL_SOCKET, SO_REUSEADDR, 1)
        sock.bind(address)
        sock.listen(5)
    
        while True:
            client, addr = sock.accept()
            print(f"Connection {addr}")
            Thread(target=fib_handler, args=(client,), daemon=True).start()
    
    
    pool = Pool(4)
    
    
    def fib_handler(client):
        while True:
            req = client.recv(100)
            if not req:
                break
    
            n = int(req)
            future = pool.submit(fib, n)
            result = future.result()
    
            resp = str(result).encode('ascii') + b'\n'
            client.send(resp)
    
        print("Closed")
    
    
    fib_server(("", 5000))
    
    # One downside of this approach is overhead of working with (sub)processes itself.
    # We can notice that perf2 results 10 times lower comparing to the fib_server_threads program.
    # 2701 req/sec
    # 2732 req/sec
    # 2707 req/sec
    # 2764 req/sec
    # 2737 req/sec
    # But at the same time, it process pool helps to balance computations and our server would not be
    # hammered much by the heavy task

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

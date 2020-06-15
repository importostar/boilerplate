---
title: concurrent_requests (1)
date: 2020-05-07
---
Example Python program concurrent_requests (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import asyncio
* import multiprocessing.pool
* import time
* import requests
* import aiohttp
* import async_timeout
* import uvloop

## Methods

* def serial(urls=URLS, session=None):
* def parallel(urls=URLS, session=None):
* async def async_get(url, session, timeout=10):
* async def async_get_all(urls):
* def asynchronous(urls=URLS, loop=None):
* def main():

## Code

Python example

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    """Making concurrent HTTP requests.
    
    Uses `requests` library which you can get with:
    
        $ pip install requests
    
    Additionally, to make HTTP requests asynchronously you have to install these
    packages:
    
        $ pip install aiohttp cchardet aiodns uvloop
    
    """
    
    import asyncio
    import multiprocessing.pool
    import time
    
    import requests
    
    try:
        import aiohttp
        import async_timeout
    except ImportError:
        aiohttp = None
        async_timeout = None
    try:
        import uvloop
    except ImportError:
        uvloop = None
    
    
    URLS = [f'https://httpbin.org/get?id={x}' for x in range(25)]
    
    
    def serial(urls=URLS, session=None):
        """Make HTTP requests in series."""
        session = session if session else requests
        return (session.get(url).json() for url in urls)
    
    
    def parallel(urls=URLS, session=None):
        """Make HTTP requests in parallel using 8 worker threads."""
        num_threads = 8
        session = session if session else requests
        with multiprocessing.pool.ThreadPool(num_threads) as pool:
            responses = pool.imap(session.get, urls)
            for response in responses:
                yield response.json()
    
    
    async def async_get(url, session, timeout=10):
        """Make one asynchronous HTTP GET request and return its JSON content."""
        with async_timeout.timeout(timeout):
            async with session.get(url) as response:
                return await response.json()
    
    
    async def async_get_all(urls):
        """Make many asynchronous HTTP GET requests and return all their JSON
        content.
        """
        async with aiohttp.ClientSession() as session:
            tasks = [async_get(url, session) for url in urls]
            return await asyncio.gather(*tasks)
    
    
    def asynchronous(urls=URLS, loop=None):
        """Fetch all URLs in an event loop asynchronously."""
        loop = loop if loop else asyncio.get_event_loop()
        return loop.run_until_complete(async_get_all(urls))
    
    
    def main():
        _ = '=' * 4
    
        session = requests.Session()
    
        print(f'{_} SERIAL (no session persitence) {_}')
        start = time.time()
        for response in serial():  # no session
            print(response)
        end = time.time() - start
        print('Done in {0:.3f}s'.format(end))
        print()
    
        print(f'{_} SERIAL (persistent session) {_}')
        start = time.time()
        for response in serial(session=session):
            print(response)
        end = time.time() - start
        print('Done in {0:.3f}s'.format(end))
        print()
    
        print(f'{_} PARALLEL (no session persistence) {_}')
        start = time.time()
        for response in parallel():  # no session
            print(response)
        end = time.time() - start
        print('Done in {0:.3f}s'.format(end))
        print()
    
        print(f'{_} PARALLEL (persistent session) {_}')
        start = time.time()
        for response in parallel(session=session):
            print(response)
        end = time.time() - start
        print('Done in {0:.3f}s'.format(end))
        print()
    
        # the uvloop was faster than vanilla event loop
        # before Python 3.6 and recent aiohttp releases
        print(f'{_} ASYNC (uvloop, persistent session) {_}')
        if aiohttp and uvloop:
            loop = uvloop.new_event_loop()
            start = time.time()
            for response in asynchronous(loop=loop):
                print(response)
            end = time.time() - start
            print('Done in {0:.3f}s'.format(end))
        else:
            print('Try installing the uvloop Python package')
            print('\t$ pip install uvloop')
        print()
    
        print(f'{_} ASYNC (vanilla loop, persistent session) {_}')
        if aiohttp:
            loop = asyncio.get_event_loop()
            start = time.time()
            for response in asynchronous(loop=loop):
                print(response)
            end = time.time() - start
            print('Done in {0:.3f}s'.format(end))
        else:
            print('Try installing the aiohttp Python package')
            print('\t$ pip install aiohttp')
        print()
    
    
    if __name__ == '__main__':
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

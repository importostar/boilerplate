---
title: multithreading
date: 2020-05-07
---
Example Python program multithreading.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import threading
* import time

## Classes

* class myThread (threading.Thread):

## Methods

*    def __init__(self, threadID, threadname, threadcounter):
*    def run(self):
* def print_time(threadName, delay, counter):

## Code

Python example

    import threading
    import time
    
    class myThread (threading.Thread):
       def __init__(self, threadID, threadname, threadcounter):
          threading.Thread.__init__(self)
          self.threadID = threadID
          self.name = threadname
          self.counter = threadcounter
       def run(self):
          print("Starting " + self.name)
          # Get lock to synchronize threads
          threadLock.acquire()
          print_time(self.name, self.counter, 3)
          # Free lock to release next thread
          threadLock.release()
    
    def print_time(threadName, delay, counter):
       while counter:
          time.sleep(delay)
          print("%s: %s" % (threadName, time.ctime(time.time())))
          counter -= 1
    
    threadLock = threading.Lock()
    threads = []
    
    # Create new threads
    thread1 = myThread(1, "Thread-1", 1)
    thread2 = myThread(2, "Thread-2", 2)
    
    # Start new Threads
    thread1.start()
    thread2.start()
    
    # Add threads to thread list
    threads.append(thread1)
    threads.append(thread2)
    
    # Wait for all threads to complete
    for t in threads:
        t.join()
    
    print("Exiting Main Thread")

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

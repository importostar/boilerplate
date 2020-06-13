---
title: reproducer
date: 2020-05-07
---
Example Python program reproducer.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import _multiprocessing
* import multiprocessing

## Methods

* def main():

## Code

Python example

    import _multiprocessing
    import multiprocessing
    
    q = multiprocessing.Queue()
    
    COUNT = 2**15 - 1
    
    if COUNT > _multiprocessing.SemLock.SEM_VALUE_MAX:
        print('It is going to lock up')
    else:
        print('It should be fine. Wait about 2 seconds.')
    
    def main():
        for i in range(COUNT):
            q.put(i)
    
        for i in range(COUNT):
            q.get(i)
    
    main()
    
    # This is the sample when it locks up.
    
    #2907 Thread_25011567   DispatchQueue_1: com.apple.main-thread  (serial) ########## <---------------------- main thread, blocked on acquire of semaphore in .put (self._sem of Queue)
    #+ 2907 start  (in libdyld.dylib) + 1  [0x7fff895f55c9]
    #+   2907 Py_Main  (in Python) + 3051  [0x10b90eb23]
    #+     2907 PyRun_SimpleFileExFlags  (in Python) + 769  [0x10b8fd3fd]
    #+       2907 PyRun_FileExFlags  (in Python) + 133  [0x10b8fd860]
    #+         2907 ???  (in Python)  load address 0x10b85a000 + 0xa37bd  [0x10b8fd7bd]
    #+           2907 PyEval_EvalCode  (in Python) + 54  [0x10b8dd7d7]
    #+             2907 PyEval_EvalCodeEx  (in Python) + 1413  [0x10b8ddd62]
    #+               2907 PyEval_EvalFrameEx  (in Python) + 13389  [0x10b8e13e3]
    #+                 2907 ???  (in Python)  load address 0x10b85a000 + 0x8a57d  [0x10b8e457d]
    #+                   2907 PyEval_EvalCodeEx  (in Python) + 1413  [0x10b8ddd62]
    #+                     2907 PyEval_EvalFrameEx  (in Python) + 14387  [0x10b8e17c9]
    #+                       2907 sem_wait  (in libsystem_kernel.dylib) + 10  [0x7fff827c97ba]
    #2907 Thread_25011569                                                  ############## <------------------- Queue's internal "feeder thread", blocked on a pipe write
    #  2907 thread_start  (in libsystem_pthread.dylib) + 13  [0x7fff871dd41d]
    #    2907 _pthread_start  (in libsystem_pthread.dylib) + 176  [0x7fff871df1e5]
    #      2907 _pthread_body  (in libsystem_pthread.dylib) + 131  [0x7fff871df268]
    #        2907 ???  (in Python)  load address 0x10b85a000 + 0xb6882  [0x10b910882]
    #          2907 PyEval_CallObjectWithKeywords  (in Python) + 93  [0x10b8e3d6b]
    #            2907 PyObject_Call  (in Python) + 99  [0x10b8642ac]
    #              2907 ???  (in Python)  load address 0x10b85a000 + 0x150cf  [0x10b86f0cf]
    #                2907 PyObject_Call  (in Python) + 99  [0x10b8642ac]
    #                  2907 ???  (in Python)  load address 0x10b85a000 + 0x2830a  [0x10b88230a]
    #                    2907 PyEval_EvalCodeEx  (in Python) + 1413  [0x10b8ddd62]
    #                      2907 PyEval_EvalFrameEx  (in Python) + 13389  [0x10b8e13e3]
    #                        2907 ???  (in Python)  load address 0x10b85a000 + 0x8a60e  [0x10b8e460e]
    #                          2907 PyEval_EvalFrameEx  (in Python) + 13389  [0x10b8e13e3]
    #                            2907 ???  (in Python)  load address 0x10b85a000 + 0x8a60e  [0x10b8e460e]
    #                              2907 PyEval_EvalFrameEx  (in Python) + 10788  [0x10b8e09ba]
    #                                2907 PyObject_Call  (in Python) + 99  [0x10b8642ac]
    #                                  2907 ???  (in Python)  load address 0x10b85a000 + 0x2830a  [0x10b88230a]
    #                                    2907 PyEval_EvalCodeEx  (in Python) + 1413  [0x10b8ddd62]
    #                                      2907 PyEval_EvalFrameEx  (in Python) + 15766  [0x10b8e1d2c]
    #                                        2907 ???  (in _multiprocessing.so)  load address 0x10bbdc000 + 0x13c0  [0x10bbdd3c0]
    #                                          2907 ???  (in _multiprocessing.so)  load address 0x10bbdc000 + 0x1a2d  [0x10bbdda2d]
    #                                            2907 write  (in libsystem_kernel.dylib) + 10  [0x7fff827c9c22]

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

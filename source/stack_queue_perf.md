---
title: stack_queue_perf
date: 2020-05-07
---
Example Python program stack_queue_perf.py

## Modules

* from collections import deque
* import logging
* from queue import Queue
* import time
* import typing as t
* import matplotlib
* import matplotlib.axes._subplots
* import matplotlib.pyplot as plt
* import matplotlib.ticker
* import numpy as np

## Code

Python example

    # based on
    # https://qiita.com/saba/items/107c4237206e31acdbef
    # Pythonのスタックとキューには何を使えばいいのか（各データ構造の速度比較）
    # by @saba (https://qiita.com/saba)
    
    from collections import deque
    import logging
    from queue import Queue
    import time
    import typing as t
    
    import matplotlib
    import matplotlib.axes._subplots
    import matplotlib.pyplot as plt
    import matplotlib.ticker
    
    import numpy as np
    
    # n_iters = np.logspace(start=2.0, stop=6.0, num=41)
    n_iters = np.logspace(start=2.0, stop=5.0, num=31)
    n_iters = list(map(int, n_iters))
    
    logger = logging.getLogger(__name__)
    logging.basicConfig(level=logging.INFO)
    
    logger.info('stack(list)')
    
    stack_list_append = []
    stack_list_pop = []
    for n_iter in n_iters:
        logger.debug(f'{n_iter} add')
        start = time.time()
        stack_list = []
        for i in range(n_iter):
            stack_list.append(i)
        stack_list_append.append(time.time() - start)
    
        logger.debug(f'{n_iter} del')
        start = time.time()
        for i in range(n_iter):
            stack_list.pop()
    
        stack_list_pop.append(time.time() - start)
    
    logger.info('stack(deque)')
    
    stack_deque_append = []
    stack_deque_pop = []
    for n_iter in n_iters:
        logger.debug(f'{n_iter} add')
        start = time.time()
        stack_deque = deque([])
        for i in range(n_iter):
            stack_deque.append(i)
        stack_deque_append.append(time.time() - start)
    
        logger.debug(f'{n_iter} del')
        start = time.time()
        for i in range(n_iter):
            stack_deque.pop()
    
        stack_deque_pop.append(time.time() - start)
    
    logger.info('queue(list)')
    
    queue_list_append = []
    queue_list_pop = []
    for n_iter in n_iters:
        logger.debug(f'{n_iter} add')
        start = time.time()
        queue_list = []
        for i in range(n_iter):
            queue_list.append(i)
        queue_list_append.append(time.time() - start)
    
        logger.debug(f'{n_iter} del')
        start = time.time()
        for i in range(n_iter):
            queue_list.pop(0)
    
        queue_list_pop.append(time.time() - start)
    
    logger.info('queue(deque)')
    
    queue_deque_append = []
    queue_deque_pop = []
    for n_iter in n_iters:
        logger.debug(f'{n_iter} add')
        start = time.time()
        queue_deque = deque([])
        for i in range(n_iter):
            queue_deque.append(i)
        queue_deque_append.append(time.time() - start)
    
        logger.debug(f'{n_iter} del')
        start = time.time()
        for i in range(n_iter):
            queue_deque.popleft()
    
        queue_deque_pop.append(time.time() - start)
    
    logger.info('queue(Queue)')
    
    queue_Queue_append = []
    queue_Queue_pop = []
    
    for n_iter in n_iters:
        logger.debug(f'{n_iter} add')
        start = time.time()
        queue_Queue = Queue()
        for i in range(n_iter):
            queue_Queue.put(i)
        queue_Queue_append.append(time.time() - start)
    
        logger.debug(f'{n_iter} del')
        start = time.time()
        for i in range(n_iter):
            queue_Queue.get()
    
        queue_Queue_pop.append(time.time() - start)
    
    logger.info('plots')
    
    fig, axs = plt.subplots(2, 2)
    axs: t.List[t.List[t.Union[matplotlib.axes.Axes, matplotlib.axes.Subplot]]]
    # actually:
    # axs: np.ndarray
    # axs[0, 0]: matplotlib.axes._subplots.AxesSubplot
    
    axs[0][0].loglog(n_iters, stack_list_append, '.-')
    axs[0][0].loglog(n_iters, stack_deque_append, '.-')
    axs[0][0].grid(True)
    axs[0][0].set_xticks([100, 1_000, 10_000, 100_000, 1_000_000])
    axs[0][0].yaxis.set_major_formatter(matplotlib.ticker.EngFormatter(unit='s'))
    axs[0][0].set_title('stack_append')
    axs[0][0].set_xlabel('Iterations')
    axs[0][0].set_ylabel('Time [s]')
    axs[0][0].legend(['list_append', 'deque_append'])
    
    axs[0][1].loglog(n_iters, stack_list_pop, '.-')
    axs[0][1].loglog(n_iters, stack_deque_pop, '.-')
    axs[0][1].grid(True)
    axs[0][1].set_xticks([100, 1_000, 10_000, 100_000, 1_000_000])
    axs[0][1].yaxis.set_major_formatter(matplotlib.ticker.EngFormatter(unit='s'))
    axs[0][1].set_title('stack_pop')
    axs[0][1].set_xlabel('Iterations')
    axs[0][1].set_ylabel('Time [s]')
    axs[0][1].legend(['list_pop', 'deque_pop'])
    
    axs[1][0].loglog(n_iters, queue_list_append, '.-')
    axs[1][0].loglog(n_iters, queue_deque_append, '.-')
    axs[1][0].loglog(n_iters, queue_Queue_append, '.-')
    axs[1][0].grid(True)
    axs[1][0].set_xticks([100, 1_000, 10_000, 100_000, 1_000_000])
    axs[1][0].yaxis.set_major_formatter(matplotlib.ticker.EngFormatter(unit='s'))
    axs[1][0].set_title('queue_append')
    axs[1][0].set_xlabel('Iterations')
    axs[1][0].set_ylabel('Time [s]')
    axs[1][0].legend(['list_append', 'deque_append', 'Queue_append'])
    
    axs[1][1].loglog(n_iters, queue_list_pop, '.-')
    axs[1][1].loglog(n_iters, queue_deque_pop, '.-')
    axs[1][1].loglog(n_iters, queue_Queue_pop, '.-')
    axs[1][1].grid(True)
    axs[1][1].set_xticks([100, 1_000, 10_000, 100_000, 1_000_000])
    axs[1][1].yaxis.set_major_formatter(matplotlib.ticker.EngFormatter(unit='s'))
    axs[1][1].set_title('queue_pop')
    axs[1][1].set_xlabel('Iterations')
    axs[1][1].set_ylabel('Time [s]')
    axs[1][1].legend(['list_pop', 'deque_pop', 'Queue_pop'])
    
    fig.show()
    
    exit(0)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

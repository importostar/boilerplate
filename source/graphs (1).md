---
title: graphs (1)
date: 2020-05-07
---
Example Python program graphs (1).py

## Modules

* import sys
* import numpy as np
* import matplotlib
* import matplotlib.pyplot as plt
* import csv
* import datetime

## Code

Python example

    import sys
    
    import numpy as np
    import matplotlib
    import matplotlib.pyplot as plt
    import csv
    import datetime
    
    
    matplotlib.rcParams.update({'font.size': 4})
    matplotlib.rcParams.update({'lines.linewidth': 0.5})
    
    src = sys.argv[1]
    dst = sys.argv[2]
    metrics = sys.argv[3:]
    
    res = csv.reader(open(src), delimiter=',')
    start = 0
    times = []
    datetimes = []
    metric_points = [[] for m in metrics]
    for row in res:
        start = start if start is not 0 else int(row[0])
        times.append(row[0])
        datetimes.append(datetime.datetime.utcfromtimestamp(float(row[0])))
        for tup in zip(metric_points, row[2:]):
            tup[0].append(tup[1])
    
    count = 0
    
    count += 1
    fig = plt.figure(count)
    fig.autofmt_xdate()
    
    plot_base = 100 * len(metrics) + 10
    met_count = 0
    for points in metric_points:
        ax = fig.add_subplot(plot_base + met_count + 1)
        ax.plot(datetimes, points)
        plt.xlabel('time')
        plt.ylabel(metrics[met_count])
        met_count += 1
    plt.savefig('/Users/gary.dusbabek/Desktop/graphs/graph.png', dpi=400)
        
        

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

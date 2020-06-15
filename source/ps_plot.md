---
title: ps_plot
date: 2020-05-07
---
Example Python program ps_plot.py

## Modules

* import matplotlib
* import matplotlib.pyplot as plt
* import numpy as np
* import csv

## Code

Python example

    import matplotlib
    matplotlib.use('Agg')
    import matplotlib.pyplot as plt
    import numpy as np
    import csv
    
    files=[ "l1dsize.csv","l1dassoc.csv", "l2uassoc.csv", "l2usize.csv", "l3uassoc.csv", "l3usize.csv", "lsize.csv"]
    
    for filename in files:
    	with open(filename, 'r') as csvfile:
    		csvreader = csv.reader(csvfile, delimiter=';')
    		values=list(csvreader)	
    
    	# assocs or sizes
    	datapoints=[]
    	#for example 500, 1024, 3000
    	problemsizes=[]
    
    	#offset of 2 to skip headlines
    	for i in range(2, len(values)):
    		if not values[i][0] in problemsizes:
    			problemsizes.append(values[i][0])
    		if not values[i][1] in datapoints:
    			datapoints.append(values[i][1])
    
    	relcycles = []
    	tmp=[]
    	foo=1
    	for i in range(2, len(problemsizes)*len(datapoints)+2):
    		tmp.append(values[i][10])
    		if (foo % len(datapoints))==0:
    			relcycles.append(tmp)
    			tmp=[]
    		foo+=1	
    		
    
    
    	#replace ',' with '.' in relcycles for matplotlib to interpret string as float
    	for i, cyclevalues in enumerate(relcycles):
    		for j, value in enumerate(cyclevalues):
    			relcycles[i][j]=value.replace(',','.')
    
    
    	
    	#let the plotting begin
    	canvas = plt.subplot(1,1,1)
    
    	xrange = np.arange(0,len(datapoints),1)
    	for  i,dataset in enumerate(relcycles):
    		canvas.plot(xrange, dataset, label='Psize='+problemsizes[i])
    		plt.xticks(np.arange(len(datapoints)), datapoints)
    
    	#shrink canvas box
    	box = canvas.get_position()
    	canvas.set_position([box.x0, box.y0, box.width * 0.8, box.height])
    	#put legend box right
    	canvas.legend(loc='upper left', bbox_to_anchor=(1, 0.5))
    
    	plt.title(values[0][0])
    	plt.ylabel(values[1][10])
    	plt.xlabel(values[1][1])
    
    	plt.savefig(filename.replace('.csv',''))
    	plt.close()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: enron_outliers
date: 2020-05-07
---
Example Python program enron_outliers.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import pickle
* import sys
* import matplotlib.pyplot
* from feature_format import featureFormat, targetFeatureSplit
* from pprint import pprint

## Code

Python example

    #!/usr/bin/python
    
    import pickle
    import sys
    import matplotlib.pyplot
    sys.path.append("C:\Users\USER\Desktop\machinelearning\ud120-projects-master/tools/")
    from feature_format import featureFormat, targetFeatureSplit
    
    
    ### read in data dictionary, convert to numpy array
    data_dict = pickle.load( open("C:\Users\USER\Desktop\machinelearning\ud120-projects-master/final_project/final_project_dataset.pkl", "r") )
    data_dict.pop('TOTAL', 0) # column 'TOTAL' is included in data points
    features = ["salary", "bonus"]
    data = featureFormat(data_dict, features)
    
    from pprint import pprint
    outliers = []
    for key in data_dict:
        val = data_dict[key]["salary"]
        if val == 'NaN':
            continue
        outliers.append((key, val))
    outliers.sort(key=lambda x: x[1], reverse=True)
    print(outliers[:2])
    
    ### your code below
    
    
    
    
    ####### visualize a scattor plot #######
    for point in data:
        salary = point[0]
        bonus = point[1]
        matplotlib.pyplot.scatter( salary, bonus )
    
    matplotlib.pyplot.xlabel("salary")
    matplotlib.pyplot.ylabel("bonus")
    matplotlib.pyplot.show()
    ########################################

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

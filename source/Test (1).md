---
title: Test (1)
date: 2020-05-07
---
Example Python program Test (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os, shutil, time
* import json

## Code

Python example

    #No puedes escribir en un fichero que ya existe, por tanto lo primero es ver si existe el fichero y si existe lo elimino
    #para empezar "limpio"
    path = "/home/egutierrez3/Spark/Spark_notebooks/Datasets/Tweets/Sequence_files"
    ###TODO CHANGE FILES BY DIRECTORIES
    import os, shutil, time
    if os.path.exists("/home/egutierrez3/Spark/Spark_notebooks/Datasets/Tweets/Sequence_files"): 
        shutil.rmtree("/home/egutierrez3/Spark/Spark_notebooks/Datasets/Tweets/Sequence_files")
    
    
    import json
    
    t0 = time.time()
    dataRDD = sc.textFile("/home/egutierrez3/Spark/Spark_notebooks/Datasets/Tweets/tweets2.json")
    
    data = dataRDD.map(lambda x: json.loads(x))
    print("\nTwiter from " + format(data.first()['user']['name']) + " ->" +format(data.first()['text']))
    
    tt = time.time() - t0
    print("\n\n Operation completed in {} seconds".format(round(tt,3)))
    
    # Filter English Tweets
    data_filtered = data.filter(lambda t: "en" in t["lang"])
    print("\n-------------------------------FIRST DATA READ ----------------------")
    print(data_filtered.first())
    
    print("\n-------------------------------SAVING IN SEQUENCE FILE ----------------------")
    
    data_mapped = data_filtered.map(lambda x: tuple((1, x)) )\
    .saveAsSequenceFile("/home/egutierrez3/Spark/Spark_notebooks/Datasets/Tweets/Sequence_files")
    
    #data_mapped.saveAsNewAPIHadoopFile(path,"org.apache.hadoop.mapreduce.lib.output.SequenceFileOutputFormat","org.apache.hadoop.io.IntWritable","org.apache.hadoop.io.Text")
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

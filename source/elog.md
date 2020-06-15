---
title: elog
date: 2020-05-07
---
Example Python program elog.py

## Modules

* import cStringIO as StringIO
* import Image
* import redis
* from matplotlib import pyplot as plt

## Methods

* def elogshow(topic, experiment, description='', figure=None):
* def _grab_from_elog(topic):

## Code

Python example

    
    """
    Interact with the elog, focus on live plotting.
    
    TJ Lane <tjlane@stanford.edu>
    Nov 4, 2014
    """
    
    
    import cStringIO as StringIO
    import Image
    
    import redis
    from matplotlib import pyplot as plt
    
    
    # connect to the elog redis DB
    # this should probably be done as part of initializing a class, but
    # I'm keeping things as minimal as possible right now...
    
    global rdb # eww, I know
    rdb = redis.StrictRedis(host='localhost', port=6379, db=0)
    rdb.incr('num_connections') # throw an exception if bad connection
    
    
    def elogshow(topic, experiment, description='', figure=None):
        """
        Display a plot in the live elog viewer. Call this function in lieu
        of pyplot.show() or pyplot.draw() -- instead of showing your
        figure on your screen, it will publish it to the elog live
        stream.
        
        Parameters
        ----------
        topic : str
            A brief but descriptive name people can use to identify your plot.
            
        experiment : str
            A string describing your experiment. Eg. cxif7214.
            
        description : str
            A longer description of the plot that will be displayed in the elog.
        
        Optional Parameters
        -------------------
        figure : matplotlib.pyplot.Figure()
            If you have a number of active matplotlib plots in your code, pass the
            one you want to plot in the elog here.
        """
        
        # get the matplotlib plot as a string
        imgdata = StringIO.StringIO()
        if figure == None:
            plt.savefig(imgdata, format='png')
        else:
            figure.savefig(imgdata, format='png')
        imgdata.seek(0)  # rewind the data
    
        # syntax here is (redis key, hash key, hash value)
        rdb.hset(topic, 'experiment', experiment)
        rdb.hset(topic, 'description', description)
        rdb.hset(topic, 'pngimage', imgdata.read()) # img str
        rdb.expire(topic, 3600) # auto-delete after an hr    
    
        return
    
    
    def _grab_from_elog(topic):
        """
        Grab a still of the current image `topic` & display.
        """
    
        experiment  = rdb.hget(topic, 'experiment')
        description = rdb.hget(topic, 'description')
        pngimage    = rdb.hget(topic, 'pngimage')
    
        if pngimage:
            im = Image.open( StringIO.StringIO(pngimage) )
            im.show()
    
        return
    
    
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

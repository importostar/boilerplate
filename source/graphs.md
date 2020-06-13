---
title: graphs
date: 2020-05-07
---
Example Python program graphs.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import matplotlib.pyplot
* import datetime

## Methods

* def plot():

## Code

Python example

    import matplotlib.pyplot
    import datetime
    
    x = []
    height = []
    humidity = []
     
    readFile = open("C:\Users\Keith\Documents\data.txt", "r")
     
    max_altitude = 0
    flight_duration = 0
     
    for line in readFile:
     
        datastring = line.split(',')
    
        callsign = datastring[0]
    
        callsign = str(callsign[2:])
    
        time_str = str(datastring[2])
        altitude = float(datastring[5])
        humidity_result = float(datastring[11])
     
        hours = int(time_str[0:2])
        minutes = int(time_str[2:4])
        seconds = int(time_str[4:6])
     
        time_obj = datetime.datetime(2013, 11, 2, hours, minutes, seconds, 0)
     
        if altitude > max_altitude:
            max_altitude = altitude
     
        x.append(time_obj)
        height.append(altitude)
        humidity.append(humidity_result)
    
    def plot():
        axes_height = matplotlib.pyplot.subplot(211)
        axes_height.set_title(str(callsign + " Altitude Data"))
        matplotlib.pyplot.plot(x, height)
        axes_humidity = matplotlib.pyplot.subplot(212)
        axes_humidity.set_title(str(callsign + " Humidity Data"))
        matplotlib.pyplot.plot(x, humidity)
        axes_humidity.set_xlabel('Time in s')
        axes_height.set_ylabel('Height in m')
        axes_humidity.set_ylabel('Velocity in m/s')
        axes_humidity.set_xlabel('Time in s')
        matplotlib.pyplot.show()
     
    readFile.close()
     
    print "Max Altitude: " + str(max_altitude)
    
    flight_duration = x[-1] - x[0]
    
    print "Flight Duration: " + str(flight_duration)
    
    plot()
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

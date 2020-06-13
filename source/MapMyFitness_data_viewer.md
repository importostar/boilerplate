---
title: MapMyFitness_data_viewer
date: 2020-05-07
---
Example Python program MapMyFitness_data_viewer.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* from mapmyfitness import MapMyFitness
* import matplotlib.pyplot as plt
* import matplotlib
* import numpy as np

## Methods

* def get_workouts():

## Code

Python example

    from mapmyfitness import MapMyFitness
    import matplotlib.pyplot as plt
    import matplotlib
    import numpy as np
    
    def get_workouts():
        # Log in
        mmf = MapMyFitness(api_key='6du8934wfvrdqnbtzd9h9kxbstdqrn2x', \
                access_token='237eee8b8f8bc541841d902ea9a533fa07b748b4')
    
        # get all workouts
        workouts = mmf.workout.search(user=48155002,per_page=50000)
    
        workout_list = workouts.page(1)
    
        paces = []
        distances = []
        dates = []
    
        for i,workout in enumerate(workout_list):
            print "processing workout " + str(i+1) + " of " + str(len(workout_list))
            if 'run' in workout.activity_type.name.lower():
                distances.append(workout.distance_total/1609.344) # convert meters to miles
                paces.append(26.8224/workout.speed_avg) # convert m/s to minutes per mile
                dates.append(workout.start_datetime)
        return distances, paces, dates, workout_list
    
    if __name__ == '__main__':
    
        months   = matplotlib.dates.MonthLocator(bymonthday=15)  # every month
        monthsFmt = matplotlib.dates.DateFormatter('%b')
    
        distances, paces, dates, workouts = get_workouts()
        d = np.array([matplotlib.dates.date2num(dd) for dd in dates])
    
        fig, ax = plt.subplots()
        ax.plot_date(d,paces,'ok')
        ax.xaxis.set_major_locator(months)
        ax.xaxis.set_major_formatter(monthsFmt)
        plt.ylabel('Pace (minutes per mile)')
    
        fig, ax = plt.subplots()
        plt.plot_date(d,distances,'ok')
        ax.xaxis.set_major_locator(months)
        ax.xaxis.set_major_formatter(monthsFmt)
        plt.ylabel('Distance (miles)')

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: job plotter
date: 2020-05-07
---
Example Python program job-plotter.py

## Modules

* import argparse
* import pprint
* import yaml
* from collections import defaultdict
* import matplotlib
* import matplotlib.pyplot as plt
* import matplotlib.patches as patches

## Methods

* def overlap_exists(ilist):
* def validate_schedule(schedule):

## Code

Python example

    # A simple script to make a plot of jobs given a simple YAML file describing a scheduling of jobs at locations
    # I have various variants of this to do more complex plotting at scale, but this contains the basics
    # An example of the scheduling file is in job-schedule.yaml
    
    import argparse
    import pprint
    import yaml
    
    parser = argparse.ArgumentParser(description='Plots a schedule of jobs from a YAML input')
    parser.add_argument('schedule', help='YAML file of job output')
    
    args = parser.parse_args()
    schedule = yaml.load(open(args.schedule).read())
    
    
    # Checks a list of intervals and determines whether or not there is an overlap
    def overlap_exists(ilist):
        ilist_sorted = sorted(ilist, key=lambda x: x[0])
        for i in range(1, len(ilist_sorted)):
            if ilist_sorted[i][0] <= ilist_sorted[i-1][1]:
                return True
        return False
    
    def validate_schedule(schedule):
        locations = set(schedule['locations'])
    
        # Assert that names are not repeated
        names = [job['name'] for job in schedule['jobs']]
        assert len(names) == len(set(names))
    
        # Assert that locations are valid
        for job in schedule['jobs']:
            assert job['location'] in locations
    
        # Assert that no two intervals overlap in any location
        from collections import defaultdict
        intervals_at_location = defaultdict(list)
        for job in schedule['jobs']:
            intervals_at_location[job['location']].append((job['start-time'], job['start-time']+job['duration']))
    
        for loc, ivals in intervals_at_location.items():
            assert not overlap_exists(ivals)
    
    validate_schedule(schedule)
    
    import matplotlib
    matplotlib.use('Agg')
    
    import matplotlib.pyplot as plt
    import matplotlib.patches as patches
    
    font = { 'weight': 'bold', 'size': 6}
    matplotlib.rc('font', **font)
    
    fig, ax = plt.subplots()
    
    # Store y offset for a particular location
    nlocs = len(schedule['locations'])
    location_yoff = {loc:(nlocs-i)*2 for i,loc in enumerate(schedule['locations'])}
    
    # Create rectangles for each job
    rectangles = {}
    for job in schedule['jobs']:
        rectangles[job['name']] = \
            patches.Rectangle((job['start-time'], location_yoff[job['location']]),
                              job['duration'], 1, facecolor='white', zorder=10)
    
    label_loc_yoff = sorted([x+0.5 for x in location_yoff.values()])
    
    # Create timeline bars for each location
    for yoff in label_loc_yoff:
        plt.axhline(y=yoff, color='black')
    
    # Plot the rectangles and text
    for r in rectangles:
        ax.add_artist(rectangles[r])
        rx, ry = rectangles[r].get_xy()
        cx = rx + rectangles[r].get_width()/2.0
        cy = ry + rectangles[r].get_height()/2.0
    
        ax.annotate(r, (cx, cy), color='black', weight='bold',
                    fontsize=6, ha='center', va='center', zorder=11)
    
    max_time = max([job['start-time']+job['duration'] for job in schedule['jobs']])
    ax.set_xlim((0, max_time*(1.05)))
    ax.set_ylim((0, 2*(nlocs+1)))
    
    # Make the plot prettier
    ax.set_aspect('equal')
    ax.spines['right'].set_visible(False)
    ax.spines['left'].set_visible(False)
    ax.spines['top'].set_visible(False)
    ax.set_yticks(label_loc_yoff)
    ax.set_yticklabels(list(reversed(schedule['locations'])))
    plt.tick_params(axis='y', which='both', right='off')
    plt.tick_params(axis='x', which='both', top='off')
    
    # Save the plot
    plt.savefig("test.pdf")

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

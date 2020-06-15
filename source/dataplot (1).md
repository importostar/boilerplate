---
title: dataplot (1)
date: 2020-05-07
---
Example Python program dataplot (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import matplotlib.pyplot, sys

## Classes

* class plotting:

## Methods

* def get_info(self):
* def __init__(self):

## Code

Python example

    #Run pip3 install matplotlib
    import matplotlib.pyplot, sys
    
    class plotting:
        def get_info(self):
            try:
                #Opens data file
                working_file = open('employmentdata.txt', 'r')
            except FileNotFoundError:
                print('File doesn\'t exist.')
                sys.exit()
            
            #Gets all lines
            all_info = working_file.readlines()
            country_name = all_info[0].rstrip('\n')
            #Gets label name for plot
            self.label = 'Employment rate of ' + country_name
            #All other lines are numbers
            string_employment_info = all_info[1:]
    
            self.employment_data = list()
            for each_year in string_employment_info:
                real_stat = float(each_year.rstrip('\n'))
                self.employment_data.append(real_stat)
            working_file.close()
    
        def __init__(self):
            self.get_info()
            print(self.employment_data)
            #numbers are plotted and plot is titled
            matplotlib.pyplot.plot([self.employment_data[-1], self.employment_data[-2], self.employment_data[-3], self.employment_data[-4], self.employment_data[-5]])
            matplotlib.pyplot.ylabel(self.label)
            matplotlib.pyplot.show()
    
    if __name__ == '__main__':
        try:
            instance = plotting()
        except(EOFError, KeyboardInterrupt, ValueError):
            print('Ending employment plotting program.')
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

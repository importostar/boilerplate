---
title: argparser
date: 2020-05-07
---
Example Python program argparser.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import argparse

## Methods

* def get_args():
* def main():

## Code

Python example

    import argparse
    
    def get_args():
        ''' create description of task '''
        parser = argparse.ArgumentParser(description='File I/O')
    
        ''' add the items of argument '''
        input = parser.add_argument_group('input', 'the path of input data')
        input.add_argument(
            '-i',
            '--input',
            type = str,
            help = "full path to data files",
            required = True)
    
        output = parser.add_argument_group('output', 'output data')
        output.add_argument(
            '-o',
            '--output',
            type = str,
            help = "output path",
            required = True)
    
        count = parser.add_argument_group('count', 'the number of count')
        count.add_argument(
            '-c',
            '--count',
            type = int,
            help = "a number",
            required = False)
        
        all = parser.add_argument_group('all', 'all of packages')
        all.add_argument(
            '-a',
            '--all',
            action = 'store_true',
            help = "install all of packages")
    
        ''' array for all arguments passed to script '''
        args = parser.parse_args()
    
        ''' assign the args to variables '''
        input_data = args.input
        output_data = args.output
        count_data = args.count
        if args.all:
            print("all: true")
        else:
            print("all: false")
    
        return input_data, output_data, count_data
        
    def main():
        i, o, c = get_args()
    
        print("input: " + i)
        print("output: " + o)
        print("count: " + str(c))
    
    if __name__ == '__main__':
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

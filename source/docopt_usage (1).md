---
title: docopt_usage (1)
date: 2020-05-07
---
Example Python program docopt_usage (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from docopt import docopt
* import argparse

## Code

Python example

    usage = '''
    === Google PAA CLI Usage ===
    Usage:
        google_paa.py query <keyword> [--num=<qnum>] [--output=<filename>] [--headless] [--cleantext]
        google_paa.py (-h | --help)
    
    Options:
        -h --help             Show this message and exit
        --output=<filename>   Filename for saving the csv output [default: ./output/paa_results.csv]
        --num=<qnum>          The number of questions to be crawled for each query [default: 20]
        
    Examples:
        google_paa.py query "truck driver"              Search "truck driver" and output to a csv file with default name
        google_paa.py query "input/queries.txt"         Search all the queries specified in "queries.txt"
        google_paa.py query "truck driver" --headless   Search headlessly 
        google_paa.py query "truck driver" --cleantext  Search "truck driver" and clean the answer text before output 
        google_paa.py query "truck driver" --num=10     Search and output 10 questions for "truck driver"
        google_paa.py query "truck driver" --output="out.csv"  Search "truck driver" and output to "out.csv"
        google_paa.py -h                                Print this message
    
    '''
    from docopt import docopt
    
    args = docopt(usage)
    print(args)
    
    
    import argparse
    parser = argparse.ArgumentParser(description="test")
    parser.add_argument("--input", default="temp.txt", help="input file name")
    args = parser.parse_args()
    print(args.input)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

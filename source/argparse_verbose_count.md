---
title: argparse_verbose_count
date: 2020-05-07
---
Example Python program argparse_verbose_count.py

## Modules

* import argparse
* import logging

## Methods

* def verbose_to_loglevel(verbose=0):
* def loglevel_to_verbose(loglevel=logging.WARNING):
* def main():

## Code

Python example

    import argparse
    import logging
    
    
    def verbose_to_loglevel(verbose=0):
        loglevel = logging.WARNING
        if verbose == 1:
            loglevel = logging.INFO
        elif verbose >= 2:
            loglevel = logging.DEBUG
        return loglevel
    
    
    # this is really useful like ['--verbose'] * verbose
    # so you interpolate it into command list
    # ['command', *(['--verbose'] * verbose)]
    def loglevel_to_verbose(loglevel=logging.WARNING):
        if loglevel >= logging.WARNING:
            verbose = 0
        elif loglevel == logging.INFO:
            verbose = 1
        elif loglevel < logging.INFO:
            verbose = 2
        return verbose
    
    
    def main():
        options_parser = argparse.ArgumentParser()
        # this allows you to parse `-v`, `-vv`, `-v -v`
        options_parser.add_argument(
            '-v',
            '--verbose',
            help='Log Verbose Messages',
            action='count',
            default=0)
        options = options_parser.parse_args()
        logging.basicConfig(level=verbose_to_loglevel(options.verbose))
    
    
    if __name__ == '__main__':
        main()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

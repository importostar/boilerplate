---
title: array match
date: 2020-05-07
---
Example Python program array-match.py

## Modules

* # this is a list with the match strings in order of importance for matching

## Methods

* def parseArrayName(storage_system):

## Code

Python example

    def parseArrayName(storage_system):
        """ This is a super-ugly piece of code, but it's necessary 
            to match all the hand-entered weirdness of the array names
            in command director.
        """
        # this is a list with the match strings in order of importance for matching
        regexps = ['[^a-zA-Z0-9](\d{5})[^a-zA-Z0-9]', # 5 digit serial surounded by non-word
                     '[^a-zA-Z0-9](\d{5})$', # 5 digit serial at the end of a line
                     '[^a-zA-Z0-9](\d{8})[^a-zA-Z0-9]*',# 8 digit serial surounded
                     '(\d{8})$', # 8 digit serial at the end of a line
                     '^(\w+-\d{2})[_-](\w+)', # "arrayname-15_model"
                     '^([a-zA-Z0-9]+)[_-]([a-zA-Z0-9]+)' # "arrayname_model" or "arrayname-model"
                     ]
        array = {}
        for search in regexps:
            match = re.search(search, storage_system)
            if match:
                # if there are 2 match groups, assume this is name-model match
                matches = match.groups()
    
                if len(matches) > 1:
                    array['name'] = matches[0]
                    array['model'] = matches[1]
                else: # else assume it's just serial.
                    array['serial'] = matches[0]
                return array
        
        return None

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

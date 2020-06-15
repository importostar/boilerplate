---
title: io
date: 2020-05-07
---
Example Python program io.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import json
* import pickle
* import readline

## Methods

* def json_from_file(filepath):
* def json_to_file(filepath, payload):
* def pkl_from_file(filepath):
* def pkl_to_file(filepath, payload):
* def prefilled_prompt(prompt, prefill=''):
* def set_from_file(filepath):
* def str_from_file(filepath):
* def str_to_file(filepath, payload):

## Code

Python example

    import json
    import pickle
    import readline
    
    #---JSON--------------------------------------------------------------------------------
    
    def json_from_file(filepath):
        try:
            with open(filepath, 'r') as f:
                return json.load(f)
        except Exception as e:
            print('Error occured while reading {} as json\n{}'.format(filepath, e.args))
    
    def json_to_file(filepath, payload):
        try:
            with open(filepath, 'w') as f:
                json.dump(payload, f, indent=4)
        except Exception as e:
            print('Error occured while writing json to {}\n{}'.format(filepath, e.args))
            
    #---PKL---------------------------------------------------------------------------------
            
    def pkl_from_file(filepath):
        try:
            with open(filepath, 'rb') as p:
                if os.path.getsize(filepath) > 0:
                    return pickle.load(p)
        except FileNotFoundError:
            print('{0} not found'.format(filepath))
        except Exception as e:
            print('Error occured while reading {} as pkl\n{}'.format(filepath, e.args))
    
    def pkl_to_file(filepath, payload):
        try:
            with open(filepath, 'wb') as out_stream:
                pickle.dump(payload, out_stream, pickle.HIGHEST_PROTOCOL)
        except Exception as e:
            print('Error occured while writing pkl to {}\n{}'.format(filepath, e.args))
    
    #---USER INPUT--------------------------------------------------------------------------        
    
    def prefilled_prompt(prompt, prefill=''):
        """
        :type prompt: str
        :type prefill: str
        Prompt user for input just like built-in input
        Value of prompt param is the prompt description, eg input('Prompt description')
        Value of prefill param is used to populate the input field prior to user prompt and can be edited by the user
        """
        readline.set_startup_hook(lambda: readline.insert_text(prefill))
        try:
            return input(prompt)
        finally:
            readline.set_startup_hook()
            
    #---SETS--------------------------------------------------------------------------------
            
    def set_from_file(filepath):
        try:
            with open(filepath, 'r') as f:
                return set([line.strip() for line in f.readlines()])
        except Exception as e:
            print('Error occured while reading {} as set\n{}'.format(filepath, e.args))
    
    #---STR---------------------------------------------------------------------------------
    
    def str_from_file(filepath):
        try:
            with open(filepath, 'r') as f:
                return f.read()
        except Exception as e:
            print('Error occured while reading {} as string\n{}'.format(filepath, e.args))
            
    def str_to_file(filepath, payload):
        try:
            with open(filepath, 'w') as f:
                f.write(payload)
        except Exception as e:
            print('Error occured while writing string to {}\n{}'.format(filepath, e.args))

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

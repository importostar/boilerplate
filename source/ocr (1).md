---
title: ocr (1)
date: 2020-05-07
---
Example Python program ocr (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import re
* import pytesseract
* import pillow
* from fuzzywuzzy import fuzz  # https://stackoverflow.com/a/28467760
* from dateutil import parser

## Code

Python example

    # install tesseract per instructions for your os
    # ubuntu: sudo apt-get install tesseract-ocr
    # sudo pip install pytesseract
    # sudo pip install python-Levenshtein
    # sudo pip install fuzzywuzzy 
    # load image(s) in working directory
    
    import re
    import pytesseract
    import pillow
    from fuzzywuzzy import fuzz  # https://stackoverflow.com/a/28467760
    from dateutil import parser
    
    text = pytesseract.image_to_string(Image.open('image.jpg'))
    print(text)
    
    # write a series of try except patterns with file manipulation until it can resolve 
    # use pillow to "enhance"
    # regex? to find company and total # https://regexr.com
    # 
    # search for vendor name, total and date
    # 
    
    # vendor_list = map(lambda x: x["name"], frappe.get_list("Supplier"))
    # best_match = # reduce ? lambda x: fuzz.ratio(x 
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

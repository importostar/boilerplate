---
title: caesarCipher
date: 2020-05-07
---
Example Python program caesarCipher.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import pyperclip

## Code

Python example

    // vim: syntax=python
    
    # Caesar Cipher
    
    import pyperclip
    
    # define the const strings to compare
    encryptMode = 'encrypt'
    decryptMode = 'decrypt'
    
    # string to be convert
    message = "'LBH PNA FUBJ OYNPX VF JUVGR OL NETHZRAG,' FNVQ SVYOL, 'OHG LBH JVYY ARIRE PBAIVAPR ZR.'"
    
    # the key
    key = 13
    
    # set the wish mode
    mode = 'encrypt'
    
    # every possible symbol that can be encrypted
    LETTERS = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
    
    # the resoult messege
    translated = ''
    
    #capitalize the string in message 
    message = message.upper()
    
    # run the encryption/descryption code on each symbol in the message string
    for symbol in message:
    	if symbol in LETTERS:
    		# get the number for the symbol
    		num = LETTERS.find(symbol) # get the number of the symbol
    		if mode == encryptMode:
    			num = num + key
    		elif mode == decryptMode:
    			num = num - key
    
    		if num >= len(LETTERS):
    			num = num - len(LETTERS)
    		elif num < 0:
    			num = num + len(LETTERS)
    
    		#add the converted symbol
    		translated = translated + LETTERS[num]
    
    	else:
    		translated = translated + symbol
    
    # print the resoult
    print(translated)
    
    # copy the resoult to the clipboard
    pyperclip.copy(translated)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

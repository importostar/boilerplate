---
title: convertQT4toQT5
date: 2020-05-07
---
Example Python program convertQT4toQT5.py

## Modules

* import os, re, stat
* from PyQt5 import QtWidgets, QtCore
* 		if 'from PyQt4 import' in each.strip():
* 			line_list[num] = 'from PyQt5 import QtWidgets, QtGui, QtCore\n'

## Methods

* def fixFile(line_list):
* def convert(main_path):

## Code

Example Python PyQt program :

    import os, re, stat
    
    from PyQt5 import QtWidgets, QtCore
    main_path = 'C:/'
    
    qtWidgets_modules = dir(QtWidgets)
    qtCore_modules = dir(QtCore)
    
    def fixFile(line_list):
    	line_generator = list(line_list)
    	changed = False
    	num = -1
    
    	for each in line_generator:
    		num += 1
    		if 'from PyQt4 import' in each.strip():
    			line_list[num] = 'from PyQt5 import QtWidgets, QtGui, QtCore\n'
    			changed = True
    			continue
    
    		result = re.search('QtGui\.(\w+)', each)
    
    		if result and result.group(1) in qtWidgets_modules:
    			line_list[num] = each.replace('QtGui', 'QtWidgets')
    			changed = True
    
    		if result and result.group(1) in qtCore_modules:
    			line_list[num] = each.replace('QtGui', 'QtCore')
    			changed = True
    
    	if changed:
    		return ''.join(line_list)
    
    def convert(main_path):
    	for dirs, folders, files in os.walk(main_path):
    		for each in [x for x in files if x.endswith('.py')]:
    			file_path = os.path.join(dirs, each).replace(os.sep, '/')
    			os.chmod(file_path, stat.S_IWRITE)
    
    			with open(file_path, 'r+') as out_file:
    				line_list = out_file.readlines()
    
    			fixed_lines = fixFile(line_list)
    
    			if fixed_lines:
    				# print file_path
    
    				with open(file_path, 'w+') as out_file:
    					out_file.write(fixed_lines)
    
    convert(main_path=main_path)

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

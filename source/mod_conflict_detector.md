---
title: mod_conflict_detector
date: 2020-05-07
---
Example Python program mod_conflict_detector.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5.QtWidgets import *
* from PyQt5.QtCore import Qt
* import sys, os
* import glob
* import re
* import zipfile

## Classes

* class Example(QWidget):

## Methods

* def get_files_for_mod(modfile):
* 	def __init__(self):
* 	def initUI(self):
* 	def buttonClicked(self):

## Code

Example Python PyQt program :

    from PyQt5.QtWidgets import *
    from PyQt5.QtCore import Qt
    import sys, os
    import glob
    import re
    import zipfile
    
    def get_files_for_mod(modfile):
    	with open(modfile, 'r') as fp:
    		data = fp.read()
    		archive = re.findall(r'archive="([^"]+)"', data, re.MULTILINE)
    		path = re.findall(r'path="([^"]+)"', data, re.MULTILINE)
    		
    		parentdir = os.path.abspath(os.path.dirname(os.path.dirname(modfile)))
    		if len(archive)>0:
    			dstfile = archive[0]
    		elif len(path)>0:
    			dstfile = path[0]
    			
    		fullpath = os.path.join(parentdir, dstfile)
    		substring_count = len(fullpath) + 1
    		if not os.path.exists(fullpath):
    			print("Could not find %s" % fullpath)
    			return
    		
    		if os.path.isfile(fullpath):
    			with zipfile.ZipFile(fullpath, 'r') as zf:
    				zf_contents = [x for x in zf.namelist() if '/' in x]
    				return zf_contents
    		elif os.path.isdir(fullpath):
    			contents = []
    			for root,dir,files in os.walk(fullpath):
    				for subfile in files:
    					full_tree_path = os.path.abspath( os.path.join(root, subfile))
    					full_tree_path = full_tree_path[substring_count:]
    					if os.pathsep in full_tree_path:
    						contents.append(full_tree_path)
    			return contents
    			
    
    class Example(QWidget):
    	def __init__(self):
    		super().__init__()
    		self.initUI()
    		
    		
    	def initUI(self):
    		if len(sys.argv) <= 1:
    			mypath = str(QFileDialog.getExistingDirectory(self, "Select Directory"))
    		else:
    			mypath = sys.argv[1]
    			
    		globpath = os.path.join(mypath, '*.mod')
    		files = glob.glob(globpath)
    		
    		boxes = QVBoxLayout()
    		
    		self.checkboxes = []
    		
    		for f in files:
    			label = os.path.basename(f)
    			cbox = QCheckBox(label, self)
    			self.checkboxes.append( dict(file=f, label=label, widget=cbox) )
    			boxes.addWidget(cbox)
    			
    		btn = QPushButton('Find conflicts', self)
    		btn.clicked.connect(self.buttonClicked)
    		boxes.addWidget(btn)
    			
    		self.setLayout(boxes)
    		
    		self.setGeometry(300, 300, 250, 150)
    		self.setWindowTitle('Paradox Conflict Detector')
    		self.show()
    		
    	def buttonClicked(self):
    		modfiles = {}
    		checked_mods = []
    		for row in self.checkboxes:
    			if row['widget'].isChecked():
    				checked_mods.append(row['label'])
    				contents = get_files_for_mod(row['file'])
    				for c in contents:
    					if c in modfiles:
    						modfiles[c].append(row['label'])
    					else:
    						modfiles[c] = [ row['label'] ]
    		print(">>> Determingin conflicts for [%s]" % ', '.join(checked_mods) )
    		for paradoxcontentfilename,modfiles in modfiles.items():
    			if len(modfiles)<=1:
    				continue
    			print("conflict detected in %s with mods %s" % (paradoxcontentfilename, str(modfiles)))
    		print("\n\n\n\n")
    			
    		
    if __name__ == '__main__':
    	
    	app = QApplication(sys.argv)
    	ex = Example()
    	sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

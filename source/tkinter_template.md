---
title: tkinter_template
date: 2020-05-07
---
Example Python program tkinter_template.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tkinter
* from tkinter import filedialog
* import xml.etree.ElementTree as ET
* import os

## Classes

* class App(tkinter.Frame):

## Methods

* def __init__(self,master=None):
* def create_widgets(self):
* def get_screen_size(self,window):
* def get_window_size(self,window):
* def center_window(self,root, width, height):
* def setup(self):
* def open_file(self):
* def get_tree(self):
* def add_staves(self):
* def do_actions(self):
* def formatLines(self):
* def export_file(self):

## Code

Python tkinter example

    # -*- coding: utf-8 -*-
    import tkinter
    from tkinter import filedialog
    
    import xml.etree.ElementTree as ET
    import os
    class App(tkinter.Frame):
        def __init__(self,master=None):
            super().__init__(master)
            self.root = master
            self.pack()
            self.setup()
            self.create_widgets()
    
        def create_widgets(self):
            self.btn0 = tkinter.Button(self.root, text='选择midi文件', command=self.open_file)
            self.label1 = tkinter.Label(self.root)
            self.btn1 = tkinter.Button(self.root, text='开始导出按键亮光视频',command=self.do_actions)
            self.label2 = tkinter.Label(self.root)
            self.btn0.pack()
            self.label1.pack()
            self.btn1.pack()
            self.label2.pack()
    
        def get_screen_size(self,window):
            return window.winfo_screenwidth(), window.winfo_screenheight()
    
        def get_window_size(self,window):
            return window.winfo_reqwidth(), window.winfo_reqheight()
    
        def center_window(self,root, width, height):
            screenwidth = root.winfo_screenwidth()
            screenheight = root.winfo_screenheight()
            size = '%dx%d+%d+%d' % (width, height, (screenwidth - width) / 2, (screenheight - height) / 2)
            print(size)
            root.geometry(size)
    
        def setup(self):
            self.center_window(self.root, 600, 300)
            self.root.minsize(300, 300)
            self.root.maxsize(600, 600)
            self.root.title('美美老师请尽情使用我吧')
    
        def open_file(self):
            filename = filedialog.askopenfilename()
            print(filename)
            self.label1['text'] = filename
            self.file_path = filename
        def get_tree(self):
            self.tree = ET.parse(self.file_path)
            self.tree_root = self.tree.getroot()
        def add_staves(self):
            r = self.tree_root.findall('.//attributes')# find all attributes nodes
            el = ET.Element('staves')
            el.text = '2'
            for node in r:
                node.insert(0,el)
        def do_actions(self):
            self.get_tree()
            self.add_staves()
            self.formatLines()
            self.export_file()
        def formatLines(self):
            all_measures = self.tree_root.findall('.//measure')  # find all attributes nodes
            # print(all_measures)
    
            # for node in all_measures:
            #     node_p = node.find('print')
            #     if node_p != None:
            #         print(node_p.attrib)
            # print('====1===')
            for node in all_measures:
                node_p = node.find('print')
                if node_p != None:
                    # print(node_p)
                    if 'number' in node.attrib:
                        if 'new-system' not in node_p.attrib:
                            node_p.attrib['new-system'] = 'no'
    
                        num = int(node.attrib['number']) - 1
                        if num % 4 == 0:
                            node_p.attrib['new-system'] = 'yes'
                        else:
                            node_p.attrib['new-system'] = 'no'
                    if 'new-page' in node_p.attrib:
                        del node_p.attrib['new-page']
            # print('===2====')
            #
            # for node in all_measures:
            #     node_p = node.find('print')
            #     if node_p != None:
            #         print(node_p.attrib)
        def export_file(self):
            output_dir = os.path.dirname(self.file_path)
            origin_file_name = os.path.basename(self.file_path).split('.')[-2]
            origin_file_ext = os.path.basename(self.file_path).split('.')[-1]
            output_file_name = output_dir+'/'+origin_file_name+'_修复版.'+origin_file_ext
            self.tree.write(output_file_name)
            self.label2['text'] = '修复成功,文件存储为：\n'+output_file_name
    root = tkinter.Tk()
    app = App(master=root)
    
    
    app.mainloop()
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

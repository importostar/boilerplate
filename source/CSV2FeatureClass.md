---
title: CSV2FeatureClass
date: 2020-05-07
---
Example Python program CSV2FeatureClass.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import arcpy
* import numpy
* import os
* import Tkinter
* import tkFileDialog
* import csv

## Classes

* class MyGUI: 

## Methods

* def __init__(self):
* def select_dir(self):
* def select_file(self):
* def placeholder():
* def Print(self):
* def perform(self):

## Code

Python tkinter example

    # Cory Rahman
    # Python 2.7.8
    print "Welcome to Cory's CSV to Feature Class converter."
    print "Importing modules & loading GUI..."
    import arcpy
    import numpy
    import os
    import Tkinter
    import tkFileDialog
    import csv
    
    class MyGUI: 
        def __init__(self):
    
    #GUI!!
            # main window 
            self.main_window=Tkinter.Tk()
            
            #Create StringVar object to store file name
            self.dir = Tkinter.StringVar()
            self.dir.set('No path selected')
    
            self.file = Tkinter.StringVar()
            self.file.set('No file selected')
    
            #frames
            self.top_frame = Tkinter.Frame(self.main_window)
            self.top_frame2 = Tkinter.Frame(self.main_window)
            self.bottom_frame = Tkinter.Frame(self.main_window)
    
            # create widgets
            self.button_dir = Tkinter.Button(self.top_frame, text='Select Geodatabase', command=self.select_dir)
            self.label_dir = Tkinter.Label(self.top_frame, textvariable=self.dir)
            
            self.button_file = Tkinter.Button(self.top_frame2, text='Select Excel file (.csv): ', command=self.select_file)
            self.label_file = Tkinter.Label(self.top_frame2, textvariable=self.file)
            
            self.my_button3 = Tkinter.Button(self.bottom_frame, text='Preview', command=self.Print)
            self.my_button4 = Tkinter.Button(self.bottom_frame, text='Create Feature Class', command=self.perform)
            self.my_button6 = Tkinter.Button(self.bottom_frame, text='Exit', command=self.main_window.destroy)
            
            # pack widgets
            self.button_dir.pack(side='left') 
            self.label_dir.pack(side='left')
    
            self.button_file.pack(side='left') 
            self.label_file.pack(side='left')
            
            self.my_button3.pack(side='top')
            self.my_button4.pack(side='top')
            self.my_button6.pack(side='top')
    
            #pack frames
            self.top_frame.pack()
            self.top_frame2.pack()
            self.bottom_frame.pack()
            
            # enter the tkinter main loop 
            Tkinter.mainloop() 
    
        #create the button's callback function
        def select_dir(self):
            global dirname
            dirname = tkFileDialog.askdirectory()
            self.dir.set(dirname)
    
        def select_file(self):
            global filename
            filename = tkFileDialog.askopenfilename()
            self.file.set(filename)
    
        def placeholder():
            pass
    
        def Print(self):
            directory = self.dir.get()
            filecsv = self.file.get()
            print
            print "Clicking Create Feature Class will parse the selected CSV and create a Feature Class from the selected Geodatabase."
            print
    
    
    #ARCPY!!
        def perform(self):
            directory=self.dir.get()#path to GDB linked from GUI
            arcpy.env.overwriteOutput = True
            arcpy.env.workspace = directory#sets the arcpy workspace to the GDB path from above
            filecsv = self.file.get()
            sr = arcpy.SpatialReference('WGS 1984')#sets sr variable to coordinate system
            print "Opening Directory..."
    
            arcpy.CreateFeatureclass_management(directory, "CSV_Output", "POINT", spatial_reference = sr)#creates the Feature Class
            print "Feature Class Created"
            
            arcpy.AddField_management("CSV_Output", "City_Name", "TEXT")#Populates the feature class
            arcpy.AddField_management("CSV_Output", "Country_Name", "TEXT")#Populates the feature class
            print "Fields Added"
    
            line_number = 0
            column_number = 0
            with open(filecsv, 'rb') as f:#this opens up the excel file and stores the data in mycsv variable
                mycsv = csv.reader(f)
                mycsv = list(mycsv)
    
                with arcpy.da.InsertCursor("CSV_Output", ["SHAPE@", "City_Name", "Country_Name"]) as ic:
                    for row in mycsv:
                        City_Name = mycsv[line_number][column_number]#mycsv[0][0] gives me the City Name (row 1 column 1) from csv
                        Country_Name = mycsv[line_number][column_number+1]#mycsv[0][1] gives the Country name (row 1 column 2)
                        longitude = mycsv[line_number][column_number+2]#etc
                        latitude = mycsv[line_number][column_number+3]#etc
    
                        point_1 = arcpy.Point(latitude,longitude)#sets long and lat for below
                        
                        ic.insertRow([point_1, City_Name, Country_Name])#actually creates the point in the feature class
                        line_number+=1#Makes sure this ^ is all repeated for each row of the csv, creating a point for each row
            print 'Creation complete, Feature Class saved to ',directory
    
    #creates an instance of the MyGUI class
    my_gui=MyGUI()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

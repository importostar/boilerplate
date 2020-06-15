---
title: kml
date: 2020-05-07
---
Example Python program kml.py

## Modules

* import simplekml #the library used to map longitudes and latitudes on google earth
* import pandas #used to read spreadsheet data
* import tkinter #the library used to generate gui stuff in python
* from tkinter.filedialog import askopenfilename

## Methods

* def browse():
* def kmlFunction(outfile = "C:\\Users\Kamran\\Desktop\\Python Codes\\points.kml"): #where infile and outfile are the two parameters

## Code

Python tkinter example

    #This program takes data of longtitude and latitude from the csv file and plots the points on google earth.
    
    import simplekml #the library used to map longitudes and latitudes on google earth
    import pandas #used to read spreadsheet data
    import tkinter #the library used to generate gui stuff in python
    from tkinter.filedialog import askopenfilename
    
    def browse():
        global infile #used so that only infile information is fetched instead of executing it directly.
        infile = askopenfilename()
    
    
    def kmlFunction(outfile = "C:\\Users\Kamran\\Desktop\\Python Codes\\points.kml"): #where infile and outfile are the two parameters
        df = pandas.read_csv(infile)
        kml = simplekml.Kml()
        for lon, lat in zip(df["Longitude"], df["Latitude"]):  #zip with for used to iterate two columns
            kml.newpoint(coords= [(lon, lat)]) #15(lon),15(lat) are geological coordinates of the location.
        kml.save(outfile) # To save kml file to use in google earth use:
    
    #first 15 is longitude and second 15 is
    
    root = tkinter.Tk()
    root.title("KML Generator") #should always be inside mainloop
    label = tkinter.Label(root, text = "This program generates a KML file.") #writes a text on the box
    label.pack() #used to pack the file in it. Without this, no text will appear
    browseButton = tkinter.Button(root, text = "Browse", command=browse) #used to create a button
    browseButton.pack() #used to pack it in. Without it, the button won't appear
    kmlButton = tkinter.Button(root, text = "Generate KML", command=kmlFunction) #used to create another button
    kmlButton.pack() #used to pack it in. Without it, the button won't appear
    root.mainloop() #used to make the gui stuff stay on the screen until the closed button is pressed
    
    
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

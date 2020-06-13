---
title: rmsdPlot
date: 2020-05-07
---
Example Python program rmsdPlot.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import csv
* import matplotlib.pyplot as plt

## Code

Python example

    #!/usr/bin/env python3
    
    """
        "rmsdPlot" is a simple script written in Python 3.
    
        It takes Residue ID and RMSD by CA values from a CSV file and plots a graph.
        The graph has Residue ID on x - axis and RMSD value on y - axis.
        "csv" module is used for parsing the csv file obtained from Pymol.
        "matplotlib.pyplot" module is used to plot the graph.
        Duplicate residueID is automatically filtered.
    
        Developer - Shashank Singh (github.com/shashank9830)
        Github Gist - https://gist.github.com/Shashank9830/6157d3f93a6450bc36c9227d173cbc74
    """
    
    import sys
    import csv
    try:
        import matplotlib.pyplot as plt
    except ImportError:
        print("\n matplotlib is not installed on your system")
        print("\n Please install matplotlib module for python3")
        print("\n This script won't work without matplotlib")
        sys.exit(0)
    
    # Get the options from user
    args = sys.argv
    
    # confirm that there are only two arguments
    if len(args[1:]) != 2:
        print("\n Invalid number of arguments")
        print("\n Usage: python3 rmsdPlot.py rmsdfile.csv refChainName")
        print("\n \"rmsdfile.csv\" is the name of your CSV file containing rmsd values")
        print("\n \"refChainName\" is the name of the reference chain")
        sys.exit(0)
    
    # parse filename and reference chain name from options
    filename = args[1]
    refChain = args[2]
    tgtChain = "TargetChain"
    
    # try opening the csv file to read data
    try:
        x = [] # list for x-coordinates
        y = [] # list for y-coordinates
    
        # read the rmsdFile and add coordinates to plot
        with open(filename) as rmsdfile:
            rmsdDataItr = csv.reader(rmsdfile) # iterator for csv file
    
            print("\n File reading started...")
            print("\n Could take some time depending on file size...")
    
            # go through each line in csv file and add required data to x and y lists
            for i, each_row in enumerate(rmsdDataItr):
                if i == 0: continue # first line is ignored as it contains coulmn names
                # check if the csv file data is in correct format
                try:
                    # don't plot duplicate residueID
                    if float(each_row[2]) not in x:
                        x.append(float(each_row[2]))
                        y.append(float(each_row[4]))
                        tgtChain = str(each_row[0])
    
                # print this error if CSV data contains non numeric value in column 3 or 5
                except:
                    print("\n CSV File Error : Please check if the data is in correct format")
                    print("\n Column 3 should contain residueId")
                    print("\n Column 5 should contain rmsdResCa")
                    sys.exit(0)
    
        print("\n File reading complete... plotting graph")
    
        # plot graph
        plt.plot(x, y, linewidth=2)      # plot line graph
        plt.scatter(x, y, color="red")   # plot points
        plt.grid(True)                   # display grid
        plt.xlabel("Residue ID")         # x axis label
        plt.ylabel("RMSD by CA")         # y axis label
        plt.title("Reference -> " + refChain + " || Target -> " + tgtChain) # title of graph
        plt.show()                       # display the graph
    
    # show error if file opening fails
    except:
        print("\n Error reading " + filename)
        print("\n Check the filename and try again")
        print("\n If the filename is correct, please make sure file is in the same folder as this script")
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

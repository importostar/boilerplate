---
title: anubis
date: 2020-05-07
---
Example Python program anubis.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import csv
* import datetime
* #from datetime import date
* import pymssql
* from decimal import Decimal
* from pprint import pprint
* import urllib2
* from itertools import islice
* import math
* import numpy as np
* import matplotlib.pyplot as plt, mpld3
* import matplotlib 

## Methods

* def webster(filename,token1, token2):
* def myformat(x):
* def launch():

## Code

Python example

    import csv
    import datetime
    #from datetime import date
    import pymssql
    from decimal import Decimal
    from pprint import pprint
    import urllib2
    from itertools import islice
    import math
    import numpy as np
    import matplotlib.pyplot as plt, mpld3
    import matplotlib 
    matplotlib.use('Agg')
    
    years = matplotlib.dates.YearLocator()
    months = matplotlib.dates.MonthLocator()
    yearsFmt = matplotlib.dates.DateFormatter('%Y')
    
    ## define a function to read a csv and make a dictionary
    # the key should be in the first row
    def webster(filename,token1, token2):
        # in single quotes call a filename
        reader = csv.reader(open(filename))
    
        # d is the dictionary I make
        d = {}
        # for each row in the handle
        for row in reader:
            # the key is in column 0
            try:
                key = str(row[0])
            except:
                continue
            #print(key)
            # if the key is already in the dictionary, skip it
            if key in d:
                continue
            # otherwise key the dictionary to have in it 
            # the items surrounded by 7 to 9
            d[key] = row[token1:token2]
        # return the dictionary to the main loop!
        return d
    
    ## a way to get "4.2f" formatting in PYTHON: 
    def myformat(x):
        return ('%.2f' % x).rstrip('0').rstrip('.')
    
    ## launch the loop
    def launch():
        response = urllib2.urlopen(theurl)
        cr = csv.reader(response)
    
        # these need to be defined within the loop I think
        acceptable_values = []
        acceptable_times = []
        bad_values = []
        bad_times = []
    
        with open(theoutput,"w") as outfile:
            writer = csv.writer(outfile,quoting=csv.QUOTE_NONNUMERIC)
    
            for row in islice(cr,5,None):
    
                dt = row[thedatecol]
                try:
                    dt = datetime.datetime.strptime(row[thedatecol],dateformat)
                except ValueError:
                    writer.writerow([row[0],'',row[theflagcol],row[thetempcol],'M'])
                    continue
    
                tt = dt.timetuple()
                doy = str(tt.tm_yday + round((float(tt.tm_hour) / 24.0),2))
    
                # if the day is in the dictionary test that the value is within bounds
                if doy in d and len(d[doy]) == 2:
                    lowval = d[doy][0]
                    highval = d[doy][1]
                    
                    testvalue = float(row[thetempcol])
                    if math.isnan(testvalue) == True:
                        writer.writerow([row[0],row[thedatecol],row[theflagcol],row[thetempcol],'M'])
    
                    else:
                        testthat = float(row[thetempcol]) >= Decimal(str(lowval)) and float(row[thetempcol]) <= Decimal(str(highval))
                        #print("it's missing")
                        
                        if testthat == 1:
                            # writer.writerow([row[0],row[thedatecol],row[theflagcol],row[thetempcol],'A'])
                            acceptable_values.append(float(row[thetempcol]))
                            acceptable_times.append(dt)
                            # print("its ok")
                        else:    
                            writer.writerow([row[0],row[thedatecol],row[theflagcol],row[thetempcol],'Q'])
                            bad_times.append(dt)
    
                            # if the value is bad because it is a maximum
                            if float(row[thetempcol]) >= Decimal(str(highval)):
                                bad_values.append(Decimal(str(highval)))
                            else:
                                bad_values.append(Decimal(str(lowval)))
    
    
            # assign a figure, and create a plot with 2 axes, label them
            fig, ax = plt.subplots(1)
            ax.set_ylabel('temperature [C]')
            ax.set_xlabel('date')
    
            # plot the acceptable values in blue
            dates = matplotlib.dates.date2num(acceptable_times)
            matplotlib.pyplot.plot_date(dates,acceptable_values,'b-')
    
            # plot the unacceptable values as red squares
            dates2 = matplotlib.dates.date2num(bad_times)
            matplotlib.pyplot.plot_date(dates2,bad_values,'rs')
            fig.autofmt_xdate()
            
            plt.savefig(theplot)
    
            print("Done!")
            plt.close('all')
    
    
    ### what is needed to run the main loop
    dateformat='%Y-%m-%d %H:%M:%S'
    
    ## write out your dictionary for use here:
    d = webster('write_new_table.csv',1,3)
    
    # 2 standard deviations from the stream gauges
    # d = webster('trunk_refstands_bins_airT.csv',5,7)
    
    ######### FORMAT THIS WAY IN FUTURE BUT NOW JUST IN THE CODE
    # Goal: make a list of urls
    #url_list = []
    
    # use a try-finally to make sure you close your file.
    #try:
    #    f = open('pathtofile.txt','rb')
    #    for line in f:
    #        url_list.append('http://youtube.com/user/%s' % line)
        # do something with url list (like call a scraper, or use urllib2
    #finally:
    #    f.close()
    #######################################
    
    # ## a list of urls
    # ## url, datestring column, air temp column(s)
    lolo = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/STREAMT/LOLO/data/lolo_201_hrly.csv",2,7,8,"lolo_hourly_bad1_4sigmastream.csv","lolo_201_hrly_fig1_4sigmastream.png"]
    loma = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/STREAMT/LOMA/data/LOMA_203_hrly.csv",2,7,8, "loma_hourly_bad1_4sigmastream.csv","LOMA_203_hrly_fig1_4sigmastream.png"]
    loup = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/STREAMT/LOUP/data/loup_204_hrly.csv",2,7,8, "loup_hourly_bad1_4sigmastream.csv","loup_204_hrly_fig1_4sigmastream.png"]
    mcup = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/STREAMT/MCUP/data/MCUP_205_hrly.csv",2,7,8, "mcup_hourly_bad1_4sigmastream.csv","MCUP_205_hrly_fig1_4sigmastream.png"]
    
    # ## columns containing airtemp, urls
    cen225_15_2 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/CenMet/data/cenmet_225_15min_2012.csv",2,[9,11,13,15],[10,12,14,16],"cenmet_225_15min_2012_bad1.csv","cenmet_225_15min_2012_fig1.png"]
    cen225_15_3 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/CenMet/data/cenmet_225_15min_2013.csv",2, [9,11,13,15],[10,12,14,16],"cenmet_225_15min_2013_bad1.csv","cenmet_225_15min_2013_fig1.png"]
    cen225_15_4 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/CenMet/data/cenmet_225_15min_2014.csv",2,[9,11,13,15],[10,12,14,16],"cenmet_225_15min_2014_bad1.csv","cenmet_225_15min_2014_fig1.png"]
    cen233_5_4 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/CenMet/data/cenmet_233_a_5min_2014.csv",2,[6,8,10,12],[7,9,11,13],"cenmet_233_a_5min_2014_bad1.csv","cenmet_233_a_5min_2014_fig1.png"]
    pri226_15_2 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/PRIMET/data/primet_226_15min_2012.csv",2,[9,11,13,15,17],[10,12,14,16,18],"primet_226_15min_2012_bad1.csv","primet_226_15min_2012_fig1.png"]
    pri226_15_3 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/PRIMET/data/primet_226_15min_2013.csv",2,[9,11,13,15,17],[10,12,14,16,18],"primet_226_15min_2013_bad1.csv","primet_226_15min_2013_fig1.png"]
    #pri226_15_4 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/PRIMET/data/primet_226_15min_2014.csv",2,[9,11,13,15],[10,12,14,16],"primet_226_15min_2014_bad1.csv","primet_226_15min_2014_fig1.png"]
    pri226_5_4 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/PRIMET/data/primet_226_a_5min_2014.csv",2,[5,7,9,11],[6,8,10,12],"primet_226_a_5min_2014_bad1.csv","primet_226_a_5min_2014_fig1.png"]
    pri229_5_3 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/PRIMET/data/primet_229_5min_2013_a.csv",2,[11,13,15,17],[12,14,16,18],"primet_229_5min_2013_a_bad1.csv","primet_229_5min_2013_a_fig1.png"]
    upl227_15_2 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/UPLMET/data/uplmet_227_15min_2012.csv",2,[9,11,13,15],[10,12,14,16],"uplmet_227_15min_2012_bad1.csv","uplmet_227_15min_2012_fig1.png"]
    upl227_15_3 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/UPLMET/data/uplmet_227_15min_2013.csv",2,[9,11,13,15,17],[10,12,14,16,18],"uplmet_227_15min_2013_bad1.csv","uplmet_227_15min_2013_fig1.png"]
    upl227_15_4 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/UPLMET/data/uplmet_227_15min_2014.csv",2,[9,11,13,15,17],[10,12,14,16,18],"uplmet_227_15min_2014_bad1.csv","uplmet_227_15min_2014_fig1.png"]
    van228_15_2 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/VANMET/data/vanmet_228_15min_2012.csv",2,[9,11,13,15],[10,12,14,16],"vanmet_228_15min_2012_bad1.csv","vanmet_228_15min_2012_fig1.png"]
    van228_15_3 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/VANMET/data/vanmet_228_15min_2013.csv",2,[9,11,13,15],[10,12,14,16],"vanmet_228_15min_2013_bad1.csv","vanmet_228_15min_2013_fig1.png"]
    cs2_15_4 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/CS2MET/data/cs2met_104_15min.csv",2,6,7,"cs2met_104_15min_bad1.csv","cs2met_104_15min_fig1.png"]
    h15_15_3 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/HI15/data/hi15_208_15min_2013.csv",2,[9,11],[10,12],"hi15_208_15min_2013_bad1.csv","hi15_208_15min_2013_fig1.png"]
    
    rs02 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/RS/RS02/data/RS02_002_hrly.csv",2,7,8,"rs02_hourly_bad1_4sigmastream.csv","rs02_hourly_fig1_4sigmastream.png"]
    rs02_5 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/RS/RS02/data/RS02_90_a_5min_2014.csv",2,[6,8,10],[7,9,11],"rs02_5min_bad1_4sigmastream.csv","rs02_5min_fig1_4sigmastream.png"]
    rs86 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/RS/RS86/data/RS86_086_hrly.csv",2,7,8,"rs86_hourly_bad1_4sigmastream.csv","rs86_hourly_fig1_4sigmastream.png"]
    rs04 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/RS/RS04/data/RS04_004_hrly.csv",2,7,8,"rs04_hourly_bad1_4sigmastream.csv","rs04_hourly_fig1_4benchmarksig_4sigmastream.png"];
    rs04_5 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/RS/RS04/data/RS04_91_a_5min_2014.csv",2,[6,8,10],[7,9,11],"rs04_5min_bad1_4sigmastream.csv","rs04_5min_fig1_4sigmastream.png"]
    rs05 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/RS/RS05/data/RS05_005_hrly.csv",2,7,8,"rs05_hourly_bad1_4sigmastream.csv","rs05_hourly_fig1_4sigmastream.png"]
    rs10 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/RS/RS10/data/RS10_010_hrly.csv",2,7,8,"rs10_hourly_bad1_4sigmastream.csv","rs10_hourly_fig1_4sigmastream.png"]
    rs12 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/RS/RS12/data/RS12_012_hrly.csv",2,7,8,"rs12_hourly_bad1_4sigmastream.csv","rs12_hourly_bad1_4sigmastream.png"]
    rs04_5 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/RS/RS12/data/RS12_94_a_5min_2014.csv",2,[6,8,10],[7,9,11],"rs12_5min_bad1_4sigmastream.csv","rs12_5min_fig1_4sigmastream.png"]
    rs20 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/RS/RS20/data/RS20_020_hrly.csv",2,7,8,"rs20_hourly_bad1_4sigmastream.csv","rs20_hourly_fig1_4benchmarksig.png"]
    rs20_5 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/RS/RS20/data/RS20_95_a_5min_2014.csv",2,[6,8,10],[7,9,11],"rs20_5min_bad1_4sigmastream.csv","rs20_5min_fig1_4sigmastream.png"]
    rs26_5 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/RS/RS26/data/RS26_96_a_5min_2014.csv",2,[6,8,10],[7,9,11],"rs26_5min_bad1_4sigmastream.csv","rs26_5min_fig1_4sigmastream.png"]
    rs26 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/RS/RS26/data/RS26_026_hrly.csv",2,7,8,"rs26_hourly_bad1_4sigmastream.csv","rs26_hourly_fig1_4sigmastream.png"]
    rs38 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/RS/RS38/data/RS38_038_hrly.csv",2,7,8,"rs38_hourly_bad1_4sigmastream.csv","rs38_hourly_fig1_4sigmastream.png"]
    rs89 = ["http://andrewsforest.oregonstate.edu/lter/about/weather/portal/RS/RS89/data/RS89_089_hrly.csv",2,7,8,"rs89_hourly_bad1_4sigmastream.csv","rs89_hourly_fig1_4sigmastream.png"]
    
    ## So many stations! for just one, just make a list with 1 item:
    
    
    # urllist = [lolo, loma, loup, mcup, cen225_15_2, cen225_15_3, cen225_15_4, cen233_5_4, pri226_15_2, pri226_15_3, pri226_15_4, pri226_5_4, pri229_5_3,upl227_15_2,upl227_15_3,upl227_15_4,van228_15_2,van228_15_3,cs2_15_4,h15_15_3]
    # urllist = [pri226_5_4, pri229_5_3,upl227_15_2,upl227_15_3,upl227_15_4,van228_15_2,van228_15_3,cs2_15_4,h15_15_3, lolo, loma, loup, mcup, rs02, rs02_5, rs86, rs04, rs04_5, rs05, rs10, rs12, rs04_5, rs20, rs20_5, rs26_5, rs26, rs38, rs89]
    # urllist = [lolo, loma, loup, mcup, rs02, rs02_5, rs86, rs04, rs04_5, rs05, rs10, rs12, rs04_5, rs20, rs20_5, rs26_5, rs26, rs38, rs89]
    urllist = [lolo, loma, loup, mcup, rs02, rs02_5, rs86, rs04, rs04_5, rs05, rs10, rs12, rs04_5, rs20, rs20_5, rs26_5, rs26, rs38, rs89]
    
    for item in urllist:
        try:
            theurl = item[0]
            thedatecol = item[1]
            thetempcol = item[2]
            theflagcol = item[3]
            theoutput = item[4]
            theplot = item[5]
            launch()
        except:
            theurl = item[0]
            thedatecol = item[1]
            theoutput = item[4]
            theplot = item[5]
            for col in item[2]:
                thetempcol = col
            for othercol in item[3]:
                theflagcol = othercol
                launch()
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: listen_for_new_gracedb_wave_maps
date: 2020-05-07
---
Example Python program listen_for_new_gracedb_wave_maps.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import os, sys, optparse
* import numpy as np
* import healpy as hp
* import matplotlib
* import matplotlib.pyplot as plt
* from ligo.gracedb.rest import GraceDb, HTTPError
* from ligo.gracedb.rest import GraceDbBasic

## Methods

* def parse_commandline():

## Code

Python example

    
    import os, sys, optparse
    import numpy as np
    import healpy as hp
    
    import matplotlib
    #matplotlib.rc('text', usetex=True)
    matplotlib.use('Agg')
    matplotlib.rcParams.update({'font.size': 16})
    matplotlib.rcParams['contour.negative_linestyle'] = 'solid'
    import matplotlib.pyplot as plt
    
    from ligo.gracedb.rest import GraceDb, HTTPError
    from ligo.gracedb.rest import GraceDbBasic
    
    def parse_commandline():
        """
        Parse the options given on the command-line.
        """
        parser = optparse.OptionParser()
    
        parser.add_option("-f", "--far", help="far threshold",type=float,default=1e-7)
        parser.add_option("-t", "--type", help="trigger type",default="LowMass")
        parser.add_option("-l", "--label", help="trigger label",default="EM_READY")
        parser.add_option("-s", "--startGPS", help="start gps",type=float,default=1100000000)
        parser.add_option("-e", "--endGPS", help="end gps",type=float,default=1150000000)    
        parser.add_option("-o", "--outputDir", help="output directory",default="output")
    
        opts, args = parser.parse_args()
    
        return opts
    
    opts = parse_commandline()
    
    if not os.path.isdir(opts.outputDir):
        os.mkdir(opts.outputDir)
    
    # Instantiate client
    #g = GraceDb()
    g = GraceDbBasic()
    
    #eventString = '%s far <%.5e %.1f .. %.1f'%(opts.type,opts.far,opts.startGPS,opts.endGPS)
    #eventString = '%s %d..%d'%(opts.type,opts.startGPS,opts.endGPS)
    eventString = '%s far <%.5e %.1f .. %.1f'%(opts.label,opts.far,opts.startGPS,opts.endGPS)
    print eventString
    
    # REST API returns an iterator
    events = g.events('%s'%eventString)
    
    rm_command = "rm skymap.fits.gz*"
    os.system(rm_command)
    
    keys = ['graceid','gpstime','extra_attributes','group','links','created','far','instruments','labels','nevents','submitter','search','likelihood']
    
    txt_file = "%s/trigs.txt"%opts.outputDir
    f = open(txt_file,"w")
    gpss = []
    
    fileorder = ['LALInference_skymap.fits.gz','bayestar.fits.gz','LIB_skymap.fits.gz']
    
    for event in events:
    
        eventinfo = {}
        for key in keys:
            if not key in event: continue
            eventinfo[key] = event[key]
        eventinfo['gpstime'] = float(eventinfo['gpstime'])
    
        if eventinfo['far'] > opts.far:
            continue
    
        if len(gpss) > 0:
            dist = np.absolute(eventinfo['gpstime'] - np.array(gpss))
            if np.min(dist) < 5:
                continue
        gpss.append(eventinfo['gpstime'])
    
        ra = 0
        dec = 0
        #f.write("%.0f %.10f %.10f\n"%(gps,ra,dec))
    
        r = []
        for lvfile in fileorder:
            try:
                r = g.files(eventinfo['graceid'], lvfile)
                break
            except:
                continue
        if r == []:
            print "Download of skymaps file for %s failed..."%eventinfo['graceid']
            continue
    
        skymapfile = open('skymap.fits.gz','w')
        skymapfile.write(r.read())
        skymapfile.close()
    
        mask = hp.read_map('skymap.fits.gz')
        npix = len(mask)
        nside = hp.npix2nside(npix)
        index = np.argmax(mask)
        theta, phi = hp.pix2ang(nside, index)
        ra = phi
        dec = 0.5*np.pi - theta
    
        ra = (ra / (2*np.pi)) * 24.0
        dec = dec * (360.0/(2*np.pi))
    
        outputDir = os.path.join(opts.outputDir,eventinfo['graceid'])
        if not os.path.isdir(outputDir):
            os.mkdir(outputDir)
    
        mv_command = "mv skymap.fits.gz %s/skymap.fits.gz"%outputDir
        os.system(mv_command)
    
        plotName = os.path.join(outputDir,'mollview.png')
        hp.mollview(mask)
        plt.show()
        plt.savefig(plotName,dpi=200)
        plt.close('all')
    
        print eventinfo['graceid'], eventinfo['gpstime'], eventinfo['far'], ra, dec
    
        f.write("%.0f %.10f %.10f\n"%(eventinfo['gpstime'],ra,dec))
    
    f.close()
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

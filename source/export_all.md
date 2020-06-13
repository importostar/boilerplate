---
title: export_all
date: 2020-05-07
---
Example Python program export_all.py

## Modules

* import ROOT
* import sys
* import matplotlib
* import matplotlib.pyplot as plt
* import numpy
* import cPickle as pick

## Methods

* def convert_to_matplotlib(p):

## Code

Python example

    import ROOT
    import sys
    import matplotlib
    #matplotlib.use('QTAgg')
    import matplotlib.pyplot as plt
    import numpy
    import cPickle as pick
    
    ns = 24
    #matplotlib.rcParams.update({'font.size': ns})
    matplotlib.rc('xtick', labelsize=ns)
    matplotlib.rc('ytick', labelsize=ns)
    matplotlib.rcParams['ytick.major.pad']='8'
    #matplotlib.rc('text', usetex=True)
    
    
    def convert_to_matplotlib(p):
        curves = [] 
        hists = []
        for i in p.GetListOfPrimitives():
            if i.IsA().InheritsFrom(ROOT.RooCurve.Class()):
                curves.append(i.Clone())
            if i.IsA().InheritsFrom(ROOT.RooHist.Class()):
                hists.append(i.Clone())
        
        return curves, hists
    
    
    afile = ROOT.TFile(sys.argv[1])
    try:
        res = afile.Get("wspResult")
        ll = res.allGenericObjects() 
    except AttributeError:
        ll = ROOT.list('TObject*')()
        for k in afile.GetListOfKeys():
            ll.push_back(afile.Get(k.GetName()))
        
    print ll
    output_dict = {}
    while 1:
        if ll.size() == 0: break
        o = ll.front()
        print o
        if not o: break
        try: 
            p = o.GetListOfPrimitives().FindObject("pad1")
            output_dict[o.GetName()] = {}
            output_dict[o.GetName()]["fit"] = convert_to_matplotlib(p) 
            p = o.GetListOfPrimitives().FindObject("pad3")
            output_dict[o.GetName()]["residuals"] = convert_to_matplotlib(p) 
            convert_to_matplotlib(p)
        except: pass
        ll.pop_front()
        
    pick.dump(output_dict, open("fit_results_old.pkl", "w"))
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

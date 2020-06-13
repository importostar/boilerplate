---
title: python_template_bench
date: 2020-05-07
---
Example Python program python_template_bench.py

## Modules

* import sys, os, glob
* import benchmarker
* from benchmarker import Benchmarker
* import tenjin
* from tenjin.helpers import to_str, escape
* import mako.template

## Code

Python example

    # -*- coding: utf-8 -*-
    
    ###
    ### benchmark of Tenjin and Mako
    ###
    ### usage:
    ###    $ easy_install tenjin
    ###    $ easy_install mako
    ###    $ easy_install benchmarker
    ###    $ python python_template_bench.py -h
    ###    $ python python_template_bench.py [-q] [-n 10000] [-c 3]
    ###
    
    import sys, os, glob
    try:
        xrange
    except NameError:
        xrange = range
    
    import benchmarker
    from benchmarker import Benchmarker
    benchmarker.cmdopt.parse()
    
    
    import tenjin
    from tenjin.helpers import to_str, escape
    
    import mako.template
    
    
    ## create template files
    
    tenjin_input = r"""
    <?py # coding: utf-8 ?>
    <?py #@ARGS: title, items ?>
    <h1>${title}</h1>
    <table>
      <?py i = 0 ?>
      <?py for item in items: ?>
      <?py   i += 1 ?>
      <tr>
        <td>${i}</td>
        <td>${item}</td>
      </tr>
      <?py #endfor ?>
    </table>
    """[1:]
    
    mako_input = r"""
    # coding: utf-8
    <h1>${title}</h1>
    <table>
    <% i = 0 %>\
    % for item in items:
    <%   i += 1 %>\
      <tr>
        <td>${i}</td>
        <td>${item}</td>
      </tr>
    % endfor
    </table>
    """[1:]
    
    for x in glob.glob('example.*'):
        os.unlink(x)
    
    with open('example.tenjin', 'w') as f:
        f.write(tenjin_input)
    
    with open('example.mako', 'w') as f:
        f.write(mako_input)
    
    
    ## context data
    CONTEXT = {
        'title': u"SOS Members",
        'items': [u"Haruhi", u"Mikuru", u"Yuki", u"Kyon", u"Itsuki"],
        #'title': "SOS Members",
        #'items': ["Haruhi", "Mikuru", "Yuki", "Kyon", "Itsuki"],
    }
    
    
    ## expected output
    EXPECTED = r"""
    <h1>SOS Members</h1>
    <table>
      <tr>
        <td>1</td>
        <td>Haruhi</td>
      </tr>
      <tr>
        <td>2</td>
        <td>Mikuru</td>
      </tr>
      <tr>
        <td>3</td>
        <td>Yuki</td>
      </tr>
      <tr>
        <td>4</td>
        <td>Kyon</td>
      </tr>
      <tr>
        <td>5</td>
        <td>Itsuki</td>
      </tr>
    </table>
    """[1:]
    
    
    for bm in Benchmarker(loop=10000, cycle=3):
    
        engine = tenjin.Engine()
        with bm('Tenjin %s' % tenjin.__version__):
            #engine = tenjin.Engine()
            context = CONTEXT.copy()
            for i in xrange(bm.loop):
                output = engine.render('example.tenjin', context)
    
        assert output == EXPECTED
    
        template = mako.template.Template(filename='example.mako')
        with bm('Mako %s' % mako.__version__):
            #template = mako.template.Template(filename='example.mako')
            context = CONTEXT.copy()
            for i in xrange(bm.loop):
                output = template.render(**context)
    
        assert output == EXPECTED
    
    
    # ----------------------------------------------------------------------
    
    ###
    ### Python 2.7.3
    ###
    # $ python python_template_bench.py -q -n 10000 -c 3
    # ## benchmarker:       release 3.0.1 (for python)
    # ## python platform:   darwin [GCC 4.2.1 (Apple Inc. build 5666) (dot 3)]
    # ## python version:    2.7.3
    # ## python executable: /opt/lang/python/2.7.3/bin/python
    #
    # ## Average of 3                    user       sys     total      real
    # Tenjin 1.1.1                     0.7700    0.0033    0.7733    0.7851
    # Mako 0.7.0                       1.0133    0.0000    1.0133    1.0297
    #
    # ## Ranking                         real
    # Tenjin 1.1.1                     0.7851 (100.0%) *************************
    # Mako 0.7.0                       1.0297 ( 76.2%) *******************
    #
    # ## Ratio Matrix                    real    [01]    [02]
    # [01] Tenjin 1.1.1                0.7851  100.0%  131.2%
    # [02] Mako 0.7.0                  1.0297   76.2%  100.0%
    #
    
    ###
    ### Python 3.2.2
    ###
    # $ python python_template_bench.py -q -n 10000 -c 3
    # ## benchmarker:       release 3.0.1 (for python)
    # ## python platform:   darwin [GCC 4.2.1 (Apple Inc. build 5666) (dot 3)]
    # ## python version:    3.2.2
    # ## python executable: /opt/lang/python/3.2.2/bin/python
    #
    # ## Average of 3                    user       sys     total      real
    # Tenjin 1.1.1                     0.6533    0.0000    0.6533    0.6588
    # Mako 0.7.0                       1.1267    0.0033    1.1300    1.1312
    #
    # ## Ranking                         real
    # Tenjin 1.1.1                     0.6588 (100.0%) *************************
    # Mako 0.7.0                       1.1312 ( 58.2%) ***************
    #
    # ## Ratio Matrix                    real    [01]    [02]
    # [01] Tenjin 1.1.1                0.6588  100.0%  171.7%
    # [02] Mako 0.7.0                  1.1312   58.2%  100.0%
    #
    
    ###
    ### PyPy 1.8
    ###
    # $ pypy python_template_bench.py -q -n 10000 -c 3
    # ## benchmarker:       release 3.0.1 (for python)
    # ## python platform:   darwin [PyPy 1.8.0 with GCC 4.2.1]
    # ## python version:    2.7.2
    # ## python executable: /opt/lang/pypy/1.8/bin/pypy
    #
    # ## Average of 3                    user       sys     total      real
    # Tenjin 1.1.1                     0.5567    0.0033    0.5600    0.5617
    # Mako 0.7.0                       1.5167    0.0067    1.5233    1.5247
    #
    # ## Ranking                         real
    # Tenjin 1.1.1                     0.5617 (100.0%) *************************
    # Mako 0.7.0                       1.5247 ( 36.8%) *********
    #
    # ## Ratio Matrix                    real    [01]    [02]
    # [01] Tenjin 1.1.1                0.5617  100.0%  271.4%
    # [02] Mako 0.7.0                  1.5247   36.8%  100.0%
    #
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: playlist_updater
date: 2020-05-07
---
Example Python program playlist_updater.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import sys
* import os
* import time

## Code

Python example

    #!/usr/bin/env python
    #-*- coding: utf-8 -*-
    
    import sys
    import os
    import time
    
    if (len(sys.argv) == 1):
        print 'What folder?'
        sys.exit(1)
    
    files = os.listdir(sys.argv[1])
    html = open("song-list.html","r+")
    
    html.write(
    '''
    <!DOCTYPE html>
    <head>
        <title>Idolm@ster Radio Current Song List</title>
        <meta charset="UTF-8" />
        <link rel='shortcut icon' type='image/png' href='img/favicon.png' />
        <style type="text/css"> 
            body { font-family: 'Helvetica','Arial',sans-serif; color: #220F00; 
            font-size: 1.2em;background-color: #FAFCFF;}
        </style>
    </head>
    <body>\n
    ''' +
    '<h2>Song List (' + str(len(files)) +' files)</h2> \n'+
    'Generated at ' + time.asctime(time.localtime(time.time())) + '\n' +
    '<ul>\n'
    ) 
    
    for file in files:
        html.write('    <li>' + file + '</li>\n')
    
    html.write('    </ul>\n</body>\n')
    html.close()
    print('song-list.html generated OK')
    sys.exit(0)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

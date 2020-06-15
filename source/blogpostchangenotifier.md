---
title: blogpostchangenotifier
date: 2020-05-07
---
Example Python program blogpostchangenotifier.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import codecs
* import urllib.request
* import sys
* import time
* import os
* import tkinter
* from tkinter import messagebox
* import platform
* import winsound
* import subprocess

## Code

Python tkinter example

    # uses python3+
    
    # blogpostchangenotifier currently is working for blogspot only, probably with little change will work for other blogs
    # There are specific users who want oftenly to refresh one blog post with new info, where
    # it seems (i think so) rss is not solution for notification
    # program can be started in command line with python3 blogpostchangenotifier.py , eventually recheck what version you have on your system
    
    # by @adam222up devoted to One rope L⚡dy daughter of Almighty
    
    # INPUT in next line put link for concrete post
    url = 'http://some-traveller-somewhere.blogspot.mk/2016/01/2016-january-march.html'
    soundfile = 'phonering.wav' # <- put your preffered soundfile in same directory with script and enter it's name here, use wav file
    ###############
    
    import codecs
    import urllib.request
    import sys
    import time
    import os
    import tkinter
    from tkinter import messagebox
    import platform
    if sys.platform.startswith('win'):
        import winsound
    import subprocess
    
    
    i = 0
    
    time.sleep(1) 
    
    while True:
    
        try:
            try:
                f = codecs.open('laststate.txt', 'r', 'utf-8')
                laststatefile = f.read()
                f.close()
            except:
                laststatefile = ''
    
            headers = {}
            headers['User-Agent'] = "Mozilla/5.0 (X11; Linux i686) AppleWebKit/537.17 (KHTML, like Gecko) Chrome/24.0.1312.27 Safari/537.17"
            req = urllib.request.Request(url, headers = headers)
            resp = urllib.request.urlopen(req)
            s = str(resp.read().decode('utf-8'))
    
            firstbr = int(s.find("<h3 class='post-title entry-title' itemprop='name'>"))
            lastbr = int(s.find("Posted by"))
    
            s = s[firstbr:lastbr]
            s=re.sub('<[^>]*>', ' ', s, flags=re.UNICODE)
            s = html.unescape(s)
    
            
            if s != laststatefile:
    
                try:
                    
                    if sys.platform.startswith('linux'):
                        os.system("play %s" % soundfile.strip())
                        
                    if sys.platform.startswith('win'):
                        winsound.PlaySound(soundfile.strip(), winsound.SND_FILENAME)
    
                    if sys.platform.startswith('darwin'): 
                        return_code = subprocess.call(["afplay", soundfile.strip()])
                        
                except Exception as e:
                    print(str(e))
    
                root = tkinter.Tk()
                root.withdraw()
                messagebox.showinfo("There is new message in ", url)
                root.destroy()
                
                g = codecs.open('laststate.txt', 'w', 'utf-8')
                g.write(s)
                g.close()
            
        except Exception as e:
            print(str(e))
    
        i += 1
        print(str(i) + ': working in background...')
        time.sleep(300) #recheck on every 5 minutes
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: ping (1)
date: 2020-05-07
---
Example Python program ping (1).py

## Modules

* import re, subprocess, tkinter, threading

## Classes

* class mainForm():

## Methods

* def avg(l):
* def getPing():
* def __init__(self):
* def update_clock(self):

## Code

Python tkinter example

    import re, subprocess, tkinter, threading
    
    fontsize = 30
    fonttype = 'Helvetica'
    timeregex = r'(?<=time=)\d+(?=ms )' # regex to retrieve the # ms
    website = 'google.com' # url to ping
    pinglimit = 5 # number of pings to average
    pinginterval = 500 # ms delay between pings
    pings = [] # array to hold pings
    
    def avg(l):
        length = len(l)
        if length == 0:
            return length
        return int(sum(l) / float(len(l)))
    
    def getPing():
        cmd = ['ping', website, '-n', '1']
        startupinfo = subprocess.STARTUPINFO()
        startupinfo.dwFlags |= subprocess.STARTF_USESHOWWINDOW
        proc = subprocess.Popen(cmd, stdout=subprocess.PIPE, startupinfo=startupinfo)
        for line in proc.stdout:
            ping = re.findall(timeregex, str(line))
            if len(ping) > 0:
                if len(pings) > pinglimit:
                    del pings[0]
                pings.append(int(ping[0]))
        proc.wait()
        return "-"
    
    class mainForm():
        def __init__(self):
            self.root = tkinter.Tk()
            self.label = tkinter.Label(text='', font=(fonttype, fontsize))
            self.label.pack()
            self.update_clock()
            self.root.mainloop()
            
        def update_clock(self):
            threading.Thread(target=getPing).start()
            self.label.configure(text=str(avg(pings)))
            self.root.after(pinginterval, self.update_clock)
            
    if __name__ == '__main__':
        app = mainForm()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

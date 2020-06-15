---
title: pinger
date: 2020-05-07
---
Example Python program pinger.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* host_lists = ['important hosts.txt', 'some other hosts.txt']
* import sys
* import subprocess
* import threading
* from multiprocessing.pool import ThreadPool
* import re
* import time
* import datetime
* import Queue as queue
* import Tkinter as tkinter
* import tkMessageBox as messagebox

## Classes

* class Widget(tkinter.Widget):
* class Notebook(Widget):
* class Progressbar(Widget):
* class ui():
* class pinger(threading.Thread):

## Methods

* def _format_optdict(optdict, script=False, ignore=None):
* def _dict_from_tcltuple(ttuple, cut_minus=True):
* def _val_or_dict(options, func, *args):
* def tclobjs_to_py(adict):
* def setup_master(master=None):
* def __init__(self, master, widgetname, kw=None):
* def __init__(self, master=None, **kw):
* def add(self, child, **kw):
* def tab(self, tab_id, option=None, **kw):
* def __init__(self, master=None, **kw):
* def start(self, interval=None):
* def stop(self):
* def destroy(self):
* def __init__(self):
* def run(self):
* def get_hosts(self):
* def update_time(self, host, colour, message = None):
* def update_tabs(self, event):
* def wait_nextping(self, event):
* def __init__(self, gui):
* def run(self):
* def ping(self):

## Code

Python tkinter example

    ## Site ping check tool ##
    ##
    ## Developed and tested on Win10 with Python2.7
    ##
    ## Implemented minimal Progressbar and Notebook widgets by cutting
    ## down code from Guilherma Polo. This *should* let us work with even earlier
    ## Python versions provided that they were compiled against Tk 8.5 or later.
    ##
    ## Reads one or more files containing details of sites to ping, pings them at
    ## the defined frequency, and displays the result in a GUI.
    ##
    ## Within the host files, the last word on each line is considered to be the
    ## target, and the other words on the line are the name displayed in the GUI.
    ## It is intended that this will allow the use of local hostnames, FQDNs and
    ## IPs for targets. Lines that are blank or start with # are ignored, allowing
    ## for neat formatting and comments.
    ##
    
    ## List of files with hosts to ping
    host_lists = ['important hosts.txt', 'some other hosts.txt']
    
    ## How often to wait between pinging them all (seconds)
    frequency = 30
    
    ## How many hosts to ping concurrently
    threads = 20
    
    ## Timeout for pings (seconds)
    timeout = 1
    
    ###
    import sys
    import subprocess
    import threading
    from multiprocessing.pool import ThreadPool
    import re
    import time
    import datetime
    import Queue as queue
    import Tkinter as tkinter
    import tkMessageBox as messagebox
    ###
    _text = unicode
    _basestr = basestring
    _map = map
    _flatten = tkinter._flatten
    
    def _format_optdict(optdict, script=False, ignore=None):
        format = "%s" if not script else "{%s}"
    
        opts = []
        for opt, value in optdict.items():
            opts.append(("-%s" % opt, value))
    
        return _flatten(opts)
    
    def _dict_from_tcltuple(ttuple, cut_minus=True):
        opt_start = 1 if cut_minus else 0
    
        retdict = {}
        it = iter(ttuple)
        for opt, val in zip(it, it):
            retdict[str(opt)[opt_start:]] = val
    
        return tclobjs_to_py(retdict)
    
    def _val_or_dict(options, func, *args):
        options = _format_optdict(options)
        res = func(*(args + options))
        return _dict_from_tcltuple(res)
    
    def tclobjs_to_py(adict):
        for opt, val in adict.items():
            adict[opt] = val
    
        return adict
    
    def setup_master(master=None):
        if master is None:
            if tkinter._support_default_root:
                master = tkinter._default_root or tkinter.Tk()
            else:
                raise RuntimeError(
                        "No master specified and Tkinter is "
                        "configured to not support default root")
        return master
    
    class Widget(tkinter.Widget):
        def __init__(self, master, widgetname, kw=None):
            master = setup_master(master)
            tkinter.Widget.__init__(self, master, widgetname, kw=kw)
    
    class Notebook(Widget):
        def __init__(self, master=None, **kw):
            Widget.__init__(self, master, "ttk::notebook", kw)
    
    
        def add(self, child, **kw):
            self.tk.call(self._w, "add", child, *(_format_optdict(kw)))
    
        def tab(self, tab_id, option=None, **kw):
            if option is not None:
                kw[option] = None
            return _val_or_dict(kw, self.tk.call, self._w, "tab", tab_id)
    
    class Progressbar(Widget):
        def __init__(self, master=None, **kw):
            Widget.__init__(self, master, "ttk::progressbar", kw)
    
        def start(self, interval=None):
            self.tk.call(self._w, "start", interval)
    
        def stop(self):
            self.tk.call(self._w, "stop")
    
    class ui():
        ## called when the window is closed
        def destroy(self):
            print('Exiting!')
            self.terminate = True
            if self.pinger != None:
                self.pinger.terminate = True
    
            self.root.destroy()
    
        ## called when the class is initialised
        def __init__(self):
            global host_lists
    
            self.terminate = False
            self.pinger = None
            
            ## basic ui config        
            self.root = tkinter.Tk()
            self.root.protocol('WM_DELETE_WINDOW', self.destroy)
            self.root.resizable(0,0)
            self.root.title('Site ping tool')
            
            ## create icons
            icon_b64_title = 'R0lGODlhGAAYAIABAAAAAP///yH5BAEKAAEALAAAAAAYABgAAAJPjI+py+0GonxJ2vms0gz3+CEcBCwgeZXkpnoBdh5xLKuvfa96zusn98MFUa2iyHgb9nrFX62CS0ZpOx6NulMuj09mVFR1Uq7fhstFSaspBQA7'
            icon_b64_ok = 'R0lGODlhFAAUAIABAAD+AP///yH5BAEKAAEALAAAAAAUABQAAAIyjB+gi30LmUuxqmYzQNq+Ll0UaDCgeEZltkItO26xtr7kx1a2Oqe4/zthgI7OZOhyFAAAOw=='
            icon_b64_alert = 'R0lGODlhFAAUAIABAP4AAP///yH5BAEKAAEALAAAAAAUABQAAAIyjI+pGwAM24vKOZrsxFLzbnGaR4VdaZIMqVZsi4yG7L4weOHbPPatD9wAeT0ibRhMAgoAOw=='
            icon_b64_unknown = 'R0lGODlhFAAUAIABAP7+AP///yH5BAEKAAEALAAAAAAUABQAAAInDI6paOsP4wtNMootwLxCmoCSeJBa6WnZuZnWyrrsjNKtLdv6kqoFADs='
            self.icon_title = tkinter.PhotoImage(data = icon_b64_title)
            self.icon_ok = tkinter.PhotoImage(data = icon_b64_ok)
            self.icon_alert = tkinter.PhotoImage(data = icon_b64_alert)
            self.icon_unknown = tkinter.PhotoImage(data = icon_b64_unknown)
            
            ## window icon
            self.root.tk.call('wm', 'iconphoto', self.root._w, self.icon_title)
            
            ## widget object storage for later reference
            self.nb_widgets = dict()
            self.ip_widgets = dict()
            
            ## progress bar for next ping
            self.progress_bar = Progressbar(self.root, orient = 'horizontal', length = 100, mode = 'indeterminate')
            self.progress_text = tkinter.Label(self.root, text= 'Ping in progress')
            self.progress_bar.grid(row = 0, column = 0, sticky = 'ew')
            self.progress_text.grid(row = 0, column = 1, sticky = 'w')
            self.progress_bar.config(mode = 'indeterminate')        
            self.progress_bar.start()
            
            ## UI events
            self.root.bind('<<WaitPing>>', self.wait_nextping)
            self.root.bind('<<TabUpdate>>', self.update_tabs)
            self.root.bind('<<UpdateHost>>', self.update_time)
            
            ## notebook
            self.nb = Notebook(self.root)
            self.nb.grid(row = 1, column = 0, columnspan = 2, sticky = 'news')
            
            ## make a tab for each file
            self.all_hosts = []
            tab_id = 0
            for fname in host_lists:
            
                ## get a list of hosts
                hosts = []
                try:
                    with open(fname, 'r') as hfile:
                        content = hfile.read().splitlines()
                except:
                    messagebox.showerror('Unable to read host list', 'An error occurred while reading ' + fname + '\nDoes the file exist and can it be read by the current user?')
                    break
                    
                for line in content:
                    re_target = re.search(r'^([^#].+)\s(\S+)$', line)
                    if re_target:
                        hosts.append([re_target.group(1), re_target.group(2)])
                        self.all_hosts.append(re_target.group(2))
                
                ## move to the next file if no hosts were found
                if len(hosts) < 1:
                    print('No hosts in ' + fname)
                    messagebox.showwarning('No hosts found', 'No host entries were found while reading ' + fname + '\nIs this supposed to be a host list?')
                    break
                else:                
                    print('Found ' + str(len(hosts)) + ' hosts in ' + fname)
                
                ## make the tab for this file
                nb_frame = tkinter.Frame(self.nb)
                clean_name = re.sub(r'\_', ' ', fname)
                clean_name = re.sub(r'\..+$', '', clean_name)
                self.nb.add(nb_frame, text = clean_name.capitalize(), image = self.icon_unknown, compound = tkinter.TOP)
                self.nb_widgets[fname] = tab_id
                tab_id += 1
                
                ## make the gui elements for each host
                row = 0
                for name, address in hosts:
                    self.ip_widgets[address] = [None, None, None]
                    self.ip_widgets[address][0] = tkinter.Label(nb_frame, text = name, background = 'yellow', anchor = 'w', padx = 10)
                    self.ip_widgets[address][1] = tkinter.Label(nb_frame, text = 'No replies seen', width = 22, anchor = 'w', padx = 10)
                    self.ip_widgets[address][0].grid(row = row, column = 0, sticky = 'ew')
                    self.ip_widgets[address][1].grid(row = row, column = 1, sticky = 'ew')
                    self.ip_widgets[address][2] = self.nb_widgets[fname]
                    row += 1
                    
            if len(self.all_hosts) < 1:
                messagebox.showerror('No hosts found', 'No hosts were found in any available host list file')
    
        def run(self):
            while self.terminate == False:
                self.root.update()
            
        def get_hosts(self):
            return self.all_hosts
        
        ## update last ping time for a host
        def update_time(self, host, colour, message = None):
            try:
                self.ip_widgets[host][0].configure(background = colour)
                if message != None:
                    self.ip_widgets[host][1].configure(text = str(message))
                
                self.root.update_idletasks()
            except:
                print('Error updating time for ' + host)
        
        ## update tab icons to reflect the current state
        def update_tabs(self, event):
            bad = unknown = []
            
            ## find unknown and bad results
            for entry in self.ip_widgets.keys():
                if self.ip_widgets[entry][0]['background'] == 'yellow':
                    if not self.ip_widgets[entry][2] in unknown:
                        unknown.append(self.ip_widgets[entry][2])
                elif self.ip_widgets[entry][0]['background'] == 'red':
                    if not self.ip_widgets[entry][2] in bad:
                        bad.append(self.ip_widgets[entry][2])                
                        
            ## update tab colours
            for entry in self.nb_widgets.keys():
                if self.nb_widgets[entry] in bad:            
                    self.nb.tab(self.nb_widgets[entry], image = self.icon_alert)
                elif self.nb_widgets[entry] in unknown:
                    self.nb.tab(self.nb_widgets[entry], image = self.icon_unknown)
                else:
                    self.nb.tab(self.nb_widgets[entry], image = self.icon_ok)
            
            self.root.update_idletasks()
            
        ## wait for next ping while updating progress bar
        def wait_nextping(self, event):
            global frequency
            end = time.time() + frequency
            
            self.progress_bar.stop()
            self.progress_bar.config(mode = 'determinate', max = frequency)
            
            while time.time() < end:
                try:
                    remaining = (end - time.time()) + 1
                    self.progress_bar.config(value = (frequency - remaining))
                    remaining_text = str(datetime.timedelta(seconds = int(remaining)))
                    self.progress_text.config(text = 'Next ping in ' + remaining_text)
                    self.root.update()
                    time.sleep(0.1)
                ## if the window is closed during this we get an exception
                except:
                    return
                
            self.progress_text.config(text = 'Ping in progress')    
            self.progress_bar.config(mode = 'indeterminate')
            self.progress_bar.start()
            self.root.update()
    
    class pinger(threading.Thread):
        def __init__(self, gui):
            ## initialise self as a thread
            threading.Thread.__init__(self)
            
            self.name = 'Ping-controller'
            self.terminate = False
            self.gui = gui
            self.gui.pinger = self
            self.pq = queue.Queue()
            self.result = queue.Queue() 
            
        def run(self):
            global frequency, threads      
            
            ## populate the queue
            targets = self.gui.get_hosts()
                
            ## make a thread pool
            for i in range(threads):
                t = threading.Thread(target = self.ping, name = 'Ping-worker-' + str(i))
                t.setDaemon(True)
                t.start() 
            
            ## ping every x (defined at top)
            while self.terminate == False:
                
                ## push the queue to the workers           
                for host in targets:
                    self.pq.put(host)
                
                ## wait for them all to execute
                self.pq.join()
                
                ## pull the results out of the output queue
                res = []
                while self.result.empty() == False:
                    try:
                        res.append(self.result.get_nowait())
                    except queue.Empty:
                        break               
                
                ## check the result
                for host, result in res:
                    if result != None:
                        self.gui.update_time(host, 'green', datetime.datetime.strftime(datetime.datetime.now(), '%Y-%m-%d %H:%M:%S') + ' (' + str(result) + 'ms)')
                    else:
                        self.gui.update_time(host, 'red')
                
                ## wait before the next run. in rare cases this throws a tk
                ## exception - probably some kind of race condition
                try:
                    self.gui.root.event_generate('<<TabUpdate>>', when = 'tail')
                    self.gui.root.event_generate('<<WaitPing>>', when = 'tail')
                except:
                    pass
                time.sleep(frequency)
    
        
        def ping(self):
            global timeout
            while self.terminate == False:
                target = self.pq.get()            
    
                try:
                    if sys.platform == 'win32':
                        output = subprocess.check_output('ping -n 1 -w ' + str(timeout * 1000) + ' ' + target, shell = True, stderr=subprocess.STDOUT)
                    else:
                        output = subprocess.check_output('ping -c 1 -W ' + str(timeout) + ' ' + target, shell = True, stderr=subprocess.STDOUT)
                except subprocess.CalledProcessError, e:
                    output = e.output       
                
                ## Check the output
                re_ok = re.search(r'\(0%( packet)? loss\)', output)
                if sys.platform == 'win32':
                    re_time = re.search(r'Average = (\d+)ms', output)
                else:
                    re_time = re.search(r'rtt min\/avg.+=\s[\d\.]+\/([\d\.]+)\/', output)
                
                ## we use queues for output to avoid race conditions
                stamp = '\n[' + datetime.datetime.strftime(datetime.datetime.now(), '%Y-%m-%d %H:%M:%S') + '] '
                if re_ok and re_time:
                    print(stamp + 'Reply from ' + target)
                    self.result.put([target, re_time.group(1)])
                else:
                    print(stamp + 'NO REPLY FROM ' + target)
                    self.result.put([target, None])
                    
                self.pq.task_done()
            
    ## start here
    gui = ui()
    ping = pinger(gui)
    ping.start()
    gui.run()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

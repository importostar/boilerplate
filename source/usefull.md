---
title: usefull
date: 2020-05-07
---
Example Python program usefull.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os, time,threading, hashlib , socket , sys
* import sys
* import tkinter
* import tkinter, threading,time
* import zipfile
* from xml.etree.ElementTree import iterparse

## Classes

* class BaseCLI():
* class ServerShell():

## Methods

* def start(self):
* def noCommand(self):
* def commandNotFound(self,cmdLine):
* def cmd_exit(self,cmdLine):
* def str_between(txt,sfrom,send):
* def sleep(a):
* def openBrowser(url,timeout=0):
* def do_wellcome(self, cid):
* def proceedCommand(self,cid,command,bufs):
* def __init__(self,port):
* def server():
* def processedClient():
* def delFromCanvas(canvas,points):
* def propo(a,b,c):
* def bornInt(ival,imin=0,imax=100):
* def sha1(s):
* def sha512(s):
* def MD5(s):
* def searchInFile(aFilename,search,context = 25):
* def CreateFrmCanvas(bg=[255,255,255]):
* def setFormScreenCenter(frm ,_size=None):
* def uf_test():
* def dict_del(aDict,akey):
* def dict_get(aDict,akey,default=None):
* def dict_add(aDict,akey,aval):
* def baseN2int(str_Num, base="0123456789"):
* def int2baseN(val, b="0123456789"):
* def showmessage(message,title="MessageBox"):
* def posit():
* def rgb(r,g,b):
* def die():
* def setTimeOut(method, secodes = 1, params={}) -> object:
* def threadJob():
* def dict2txt(dt,tab=" "):
* def setInterval(method,secodes  = 1):
* def threadJob():
* def StopInterval(idInterval):
* def sec2hms(sec):
* def fileMD5trunk(afile,block=1024):
* def readXlsx( fileName, **args ):

## Code

Python tkinter example

    import os, time,threading, hashlib , socket , sys
    class BaseCLI():
        def start(self):
            self.CLI_Loop=True
            self.prompt=">"
            while self.CLI_Loop:
                print(self.prompt,end="",flush=True)
                s=sys.stdin.readline().strip()
                if s=="":
                    self.noCommand()
                    continue
                cmdLine=s.split()
                cmdLine+=['']
                m = getattr(self,"cmd_"+cmdLine[0],
                            self.commandNotFound)
                m(cmdLine)
        def noCommand(self):
            pass
        def commandNotFound(self,cmdLine):
            print(cmdLine[0],": Command not found",sep="")
        def cmd_exit(self,cmdLine):
            self.CLI_Loop=False
            print("Bye.")
    
    def str_between(txt,sfrom,send):
        return (txt+sfrom).split(sfrom)[1].split(send)[0]
    def sleep(a):
        time.sleep(a)
    
    def openBrowser(url,timeout=0):
        import sys
        setTimeOut(lambda: os.system(sys.executable + ' -m webbrowser -t "'+url+'" '), timeout)
    
    class ServerShell():
        def do_wellcome(self, cid):
            c=self.clients[cid]["client"]
            c.send(b"Wellcome\n")
        def proceedCommand(self,cid,command,bufs):
            cmds = command.strip().split(" ")
            cmd = cmds.pop(0)
            amethod=getattr(self,"cmd_"+cmd,None)
            print("Pour la commande ",cmd, "La methode est : " ,amethod)
            if callable(amethod):
                return amethod(cid,self.clients[cid]["client"],cmds)
    
        def __init__(self,port):
            self.socket=socket.socket()
            self.socket.bind(("",port))
            self.clients={}
            def server():
                self.socket.listen()
                while True:
                    cc=self.socket.accept()
                    print("New Client ",cc)
                    aClient = cc[0]
                    clientID = time.time()
                    self.clients[clientID]={"id":clientID,"client":aClient,"buf":""}
                    def processedClient():
                        print("WellCome ",clientID)
                        self.do_wellcome(clientID)
                        while True:
                            print("Wait for data for client",clientID)
                            buf = aClient.recv(1024*10).decode(errors="ignore") # type: str
                            print({"length": len(buf), "buf": buf})
                            if len(buf)==0:
                                break
                            bufs = buf.strip().split("\n")
                            while bufs !=[]:
                                s = bufs.pop(0) #type: str
                                print("Proceed",s)
                                self.proceedCommand(clientID,s,bufs)
    
                            if buf.startswith(("die","DIE")):
                                aClient.close()
                                self.socket.close()
                    setTimeOut(processedClient,0)
    
            setTimeOut(server,0)
    
    def delFromCanvas(canvas,points):
        for p in points:
            canvas.delete(p)
    def propo(a,b,c):
        return a*c+b*(1-c)
    def bornInt(ival,imin=0,imax=100):
        return imin if ival<imin else imax if ival>imax else ival
    def sha1(s):
        return hashlib.sha1(s.encode()).hexdigest()
    def sha512(s):
        return hashlib.sha512(s.encode()).hexdigest()
    def MD5(s):
        if type(s) is bytes:
            return hashlib.md5(s).hexdigest()
    
        return hashlib.md5(str(s).encode()).hexdigest()
    
    def searchInFile(aFilename,search,context = 25):
        if type(search) is str:
            search=(search,)
        bigs =0;
        sr=[]
        for s in search:
            sr.append(s.upper())
            if bigs<len(s):
                bigs=len(s)+1
        f = open(aFilename,errors="ignore")
        while True:
            buff=f.read(context*2).upper()
            for s in sr:
                if buff.find(s)!=-1:
                    print(s,": ",buff)
    
            f.seek(f.seek(0,1)-bigs)
    
            if len(buff)!=context*2:
                break
        f.close()
    
    def CreateFrmCanvas(bg=[255,255,255]):
        import tkinter
        frm=tkinter.Toplevel()
        c=tkinter.Canvas(frm,bg=rgb(bg[0],bg[1],bg[2]))
        c.pack(fill=tkinter.BOTH,expand=tkinter.YES)
        return (frm,c)
    def setFormScreenCenter(frm ,_size=None):
    
        if _size==None:
            _size=str(frm.winfo_width())+"x"+str(frm.winfo_height())
        else :
            frm.geometry(_size)
        frm.update()
        frm.geometry("+%s+%s" % (int(frm.winfo_screenwidth()//2- frm.winfo_width()//2),int(frm.winfo_screenheight()//2- frm.winfo_height()//2)))
    
    
    
    def uf_test():
        print("usefull Test")
    
    
    def dict_del(aDict,akey):
        if akey in aDict:
            del(aDict[akey])
    
    def dict_get(aDict,akey,default=None):
        if akey in aDict:
            return aDict[akey]
        return default
    
    def dict_add(aDict,akey,aval):
        if akey in aDict:
            aDict[akey]+=aval
        else:
            aDict[akey] = aval
    
    def baseN2int(str_Num, base="0123456789"):
        str_Num=str_Num.lstrip(base[0])[::-1]
        pos=0
        rst=0
        for i in str_Num:
            rst+=base.find(i)*len(base)**pos
            pos+=1
        return rst
    
    def int2baseN(val, b="0123456789"):
        nb = len(b)
        rst = ""
        if val == 0:
            return b[0]
        while val > 0:
            rst = b[val % nb] + rst
            val //= nb
        return rst
    
    def showmessage(message,title="MessageBox"):
        import tkinter, threading,time
        msg = tkinter.Tk()
        msg.title(title)
    
        lb=tkinter.Label(msg,text=str(message))
        lb.pack(fill=tkinter.BOTH,expand=tkinter.YES)
        btn = tkinter.Button(msg,text="OK",command=lambda :msg.destroy())
        btn.pack()
        def posit():
            time.sleep(0.2)
            w = 256 if msg.winfo_width()<256 else msg.winfo_width()
            h = msg.winfo_screenheight()
            t = h / 4 if msg.winfo_height() < (h - (h/4)) else (((h - (h/4))-msg.winfo_height()))
    
            geo= "%dx%d+%d+%d" % (w,
                                  100 if msg.winfo_height() < 100 else msg.winfo_height(),
                                  (msg.winfo_screenwidth()/2)-(w/2),
                                  t)
            msg.geometry(geo)
    
        threading.Thread(target=posit).start()
        msg.mainloop()
    def rgb(r,g,b):
        return "#%02X%02X%02X" % (int(r)%256,int(g)%256,int(b)%256)
    def die():
        os._exit(0)
    intervalList={}
    def setTimeOut(method, secodes = 1, params={}) -> object:
        def threadJob():
            if secodes!=0:
                time.sleep(secodes)
            if callable(method):
                if params!={}:
                    method(params)
                else:
                    method()
        threading.Thread(target=threadJob).start()
    def dict2txt(dt,tab=" "):
        if type(dt)==dict:
            st=""
            for k in dt:
                st+=tab+str(k)+":\n"+dict2txt(dt[k],tab+tab[0])+"\n"
            return st
        if type(dt)==list:
            st = ""
            for k in dt:
                st+=tab+dict2txt(k,tab+tab[0])+"\n"
            return st
        return tab+str(dt)
    
    def setInterval(method,secodes  = 1):
        if not callable(method):
            return False
        idThread = time.time()
        intervalList[idThread]=secodes
        def threadJob():
            while True:
                if idThread in intervalList:
                    if method() == False:
                        break
                    time.sleep(intervalList[idThread])
                else:
                    break
        threading.Thread(target=threadJob).start()
        return idThread
    
    def StopInterval(idInterval):
        dict_del(intervalList,idInterval)
    
    
    
    def sec2hms(sec):
        sec = int(sec)
        ssec=sec % 60
        smin = (sec % (60*60))//60
        sh = (sec)//3600
        rst = "%02dH %02dm %02ds"%(sh,smin,ssec)
        return rst
    
    def fileMD5trunk(afile,block=1024):
    
        f = open(afile,"rb")
    
        rst = []
        while True :
            b = f.read(block)
    
            if len(b)==0:
                break
            rst+=[MD5(b)]
        return rst
    #readXlsx( "mysheet.xlsx", sheet = 1, header = True )
    def readXlsx( fileName, **args ):
    
        import zipfile
        from xml.etree.ElementTree import iterparse
    
        if "sheet" in args:
           sheet=args["sheet"]
        else:
           sheet=1
        if "header" in args:
           isHeader=args["header"]
        else:
           isHeader=False
    
        rows   = []
        row    = {}
        header = {}
    
        z      = zipfile.ZipFile( fileName )
    
        # Get shared strings
        strings = [ el.text for e, el
                            in  iterparse( z.open( 'xl/sharedStrings.xml' ) )
                            if el.tag.endswith( '}t' )
                            ]
        value = ''
    
        # Open specified worksheet
        for e, el in iterparse( z.open( 'xl/worksheets/sheet%d.xml'%( sheet ) ) ):
           # get value or index to shared strings
           if el.tag.endswith( '}v' ):                                   # <v>84</v>
               value = el.text
           if el.tag.endswith( '}c' ):                                   # <c r="A3" t="s"><v>84</v></c>
    
               # If value is a shared string, use value as an index
               if el.attrib.get( 't' ) == 's':
                   value = strings[int( value )]
    
               # split the row/col information so that the row leter(s) can be separate
               letter = el.attrib['r']                                   # AZ22
               while letter[-1].isdigit():
                   letter = letter[:-1]
    
               # if it is the first row, then create a header hash for the names
               # that COULD be used
               if rows ==[]:
                   header[letter]=value
               else:
                   if value != '':
    
                       # if there is a header row, use the first row's names as the row hash index
                       if isHeader == True and letter in header:
                           row[header[letter]] = value
                       else:
                           row[letter] = value
    
               value = ''
           if el.tag.endswith('}row'):
               rows.append(row)
               row = {}
        z.close()
        return rows
    
    
    if __name__=="__main__":
        showmessage(MD5("nonohome"))
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: pdfprocessing
date: 2020-05-07
---
Example Python program pdfprocessing.py

## Modules

* import webbrowser, sys, pyperclip, os, Tkinter
* import tkFileDialog
* import pywinauto
* import subprocess
* from time import sleep
* import ahk
* import win32con
* import win32api
* # address import
* # from windowmngr import WindowMgr

## Classes

* class OCR_Methods:
* class myPDF:

## Methods

* def getfilename():
* def __init__(self):
* def add_ocr_textlayer(self,pdfname):
* def setupdirectory(basedirectory):
* def text2pdf(text,pdfname = None):
* def pdf2tif(pdfname,tifname):
* def deskewpdf(pdfname,newpdfname=None,angle=None):
* def __init__(self,pdfname=None):
* def burst_pdf(self):
* def rotate_pdf(self):
* def ocr(self):
* def get_text(self):

## Code

Python tkinter example

    # mapIt.py - Launches a map in the browser using an address from the
    # command line or clipboard.
    
    import webbrowser, sys, pyperclip, os, Tkinter
    import tkFileDialog
    import pywinauto
    import subprocess
    from time import sleep
    import ahk
    import win32con
    import win32api
    
    # address import
    # from windowmngr import WindowMgr
    #c:\gnuwin32\bin\enscript [INPUT FILENAME] -B -f fTimes-Roman10.5 -o [OUTPUT FILENAME] --wordwrap -G2rE
    
    
    
    def getfilename():
        """Use to get the name of a file using a tkinter dialog"""
        # The method used here involves the use of a withdraw command
        # this is done so that the tkinter window closes when the filedialog exits.
        root = Tkinter.Tk()
        filename = tkFileDialog.askopenfilename()
        root.withdraw()
        if filename == '':
            return None
        else:
            return filename
    
    class OCR_Methods:
        def __init__(self):
            self.programfilepaths = {
                "ghostscript": 'C:\\Program Files\\gs\\gs9.16\\bin\\gswin32c.exe',
                "enscript": 'c:/gnuwin32/bin/enscript',
                "deskew": '',
                "tesseract": '',
                "pdfXCV": "C:/Program Files/Tracker Software/PDF Viewer/PDFXCview.exe"
            }
        def add_ocr_textlayer(self,pdfname):
            """Method that uses pdf XChange Viewer.
            1. Open the file from the commandline
            2. Open the ocr options
            3. """
            programpath = self.programfilepaths['pdfXCV']
            if programpath != '':
                subprocess.Popen([programpath, pdfname])
                print programpath
                # w = WindowMgr()
                # w.find_window_wildcard(".*PDF-X.*")
                # w.set_foreground()
                sleep(3)
                ahk.execute("""
                    SetTitleMatchMode, 2
                    WinActivate, PDF-XChange
                    """)
                ahk.execute("Send, ^+C")
                for i in range(5):
                    sleep(.05)
                    ahk.execute("Send, {Tab}")
                ahk.execute('Send, {Enter}')
                sleep(.05)
                # ahk.execute("""
                #     SetTitleMatchMode, 2
                #     WinActivate, PDF-XChange
                #     """)
                #
                # while True:
                #     sleep(1)
                #     capital = win32con.VK_VOLUME_MUTE
                #     capsdown = win32api.GetKeyState(capital)
                #     if capsdown != 0:
                #         print capsdown
                #         # print win32api.GetKeyState(win32con.VK_CAPITAL)
                #         break
                root = Tkinter.Tk()
                tkFileDialog.askopenfilename()
                ahk.reload()
                print ahk.ready()
                ahk.execute("Send, ^{s}")
                sleep(1)
                ahk.execute("Send, !{f4}")
                quit()
    
    
    
    
    def setupdirectory(basedirectory):
        """Creates temporary filestructure to use in pdf processing
            cwd
             |--/temppdf (Holds bursted pdf)
             |--/deskewedpdf (Holds pdfs cleaned during deskew stage)
             |--/temptif (Holds the tif images)
             |--/textoutput (Holds textoutput for the pdf)
             |--/pdfoutput (Holds the ocred pdf if we so desire)
        """
        pass
    
    
    def text2pdf(text,pdfname = None):
        pass
        #c:\gnuwin32\bin\enscript [INPUT FILENAME] -B -f fTimes-Roman10.5 -o [OUTPUT FILENAME] --wordwrap -G2rE
    
    def pdf2tif(pdfname,tifname):
        pass
    
    def deskewpdf(pdfname,newpdfname=None,angle=None):
        pass
    
    
    
    class myPDF:
        def __init__(self,pdfname=None):
            self.pdfname = ''
            self.directory_in = ''
            self.directory_out = ''
            if pdfname is not None:
                self.pdfname = pdfname
                print self.pdfname
            else:
                self.pdfname = getfilename()
                print self.pdfname
        def burst_pdf(self):
            pass
        def rotate_pdf(self):
            pass
        def ocr(self):
            pass
        def get_text(self):
            pass
    
    # filename = getfilename()
    # if filename == None:
    #     pass
    # else:
    #     sys.stdout.write(filename)
    
    if len(sys.argv) > 1:
        filename = sys.argv[1]
    else:
        filename = getfilename()
    mymethods = OCR_Methods()
    ahk.start()
    mymethods.add_ocr_textlayer(filename)
    
    
    
    
    
    # if len(sys.argv) > 1:
    #     # Get address from command line.
    #     print sys.argv [1:]
    # else:
    #     # Get address from clipboard.
    #     # address = pyperclip.paste()
    #     filename = getfilename()
    #     if filename == '':
    
    
    
    # if __name__ == '__main__':
    #     pdf = myPDF()
    
    
    
    #         sys.stdout.write(filename)
    
    
    
    # if __name__ == '__main__':
    
    
    # webbrowser.open('https://www.google.com/maps/place/' + address)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

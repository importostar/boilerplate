---
title: yd
date: 2020-05-07
---
Example Python program yd.py

## Modules

* import tkinter as tk
* import youtube_dl as yd
* from tkinter import *
* from tkinter import messagebox, filedialog

## Methods

* def CreateWidgets():
* def Browse():
* def Download():

## Code

Python tkinter example

    import tkinter as tk
    import youtube_dl as yd
    from tkinter import *
    from tkinter import messagebox, filedialog
    
    # Defining CreateWidgets() function to create necessary tkinter widgets
    def CreateWidgets():
        linkLabel = Label(root, text="ENTER THE VIDEO LINK : ", bg="slategrey")
        linkLabel.grid(row=1, column=0, pady=5, padx=5)
    
        root.linkText = Entry(root, width=60)
        root.linkText.grid(row=1, column=1, pady=5, padx=5, columnspan = 2)
    
        destinationLabel = Label(root, text="SAVE AUDIO IN : ", bg="slategrey")
        destinationLabel.grid(row=2, column=0, pady=5, padx=5)
    
        root.destinationText = Entry(root, width=38)
        root.destinationText.grid(row=2, column=1, pady=5, padx=5)
    
        browseButton = Button(root, text="BROWSE", command=Browse, width=15)
        browseButton.grid(row=2, column=2, pady=5, padx=5)
    
        dwldButton = Button(root, text="DOWNLOAD AUDIO", command=Download, width=30)
        dwldButton.grid(row=3, column=1, pady=5, padx=5)
    
    # Defining Browse() to select a destination folder to save the audio file
    def Browse():
        # Retrieving the user-input destination directory
        root.destinationDIR= filedialog.askdirectory(initialdir="C:\Python\PyYoutubeAudio")
    
        # Displaying the directory in the directory textbox
        root.destinationText.insert('1', root.destinationDIR)
    
    # Defining Download() to download the video as audio file
    def Download():
        # Fetching and Storing the user-input video link and save path
        videoLink = root.linkText.get()
        savePath = root.destinationText.get()
    
        # Specifying the options for downloading
        audDWLDopt = {
            # Specifying to download audio in best format
            'format':'bestaudio/best',
            # Destination to save the audio file with the title as the name
            'outtmpl': savePath+"/%(title)s.%(ext)s",
            # Converting video to audio
            'postprocessors':[{
                # Extracting audio from the video
                'key':'FFmpegExtractAudio',
                # Format for saving the audio (mp3, wav)
                'preferredcodec': 'mp3',
                # Quality of the audio (Audio BitRate)
                'preferredquality': '320'
            }],
        }
        # Downloading the audio file
        with yd.YoutubeDL(audDWLDopt) as aud_dwld:
            aud_dwld.download([videoLink])
    
        messagebox.showinfo("SUCCESS", "VIDEO CONVERTED AND DOWNLOADED AS AUDIO")
    
    root = tk.Tk()
    
    # Setting the title, background color
    # and size of the tkinter window and
    root.geometry("700x700")
    root.title("Dr4 downloader haha")
    root.resizable(True, True)
    root.config(background="Black")
    
    CreateWidgets()
    
    root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

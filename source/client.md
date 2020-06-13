---
title: client
date: 2020-05-07
---
Example Python program client.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import socket,threading,tkinter,json,winsound

## Classes

* class LabelFrame(tk.LabelFrame):

## Methods

* def echo_data(sock):
* def send(event=None):
* def on_closing(event=None):
* def connect():
*    def __init__(self, parent, text):
*    def joined(self, message):
*    def connected(self, message):
*    def disjoined(self, message):

## Code

Python tkinter example

    import socket,threading,tkinter,json,winsound
    tk = tkinter
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    
    
    def echo_data(sock):
       while True:
          
          try:
             msg = sock.recv(1024).decode('utf8')
    
             if msg[0] == '{': # JSON Message
                   message = json.loads(msg)
    
                   # We don't have the `app` object, therefore you have to handle the message here
    
                   if 'CONNECTED' in message:
                      msg_list.insert(tkinter.END, "Welcome {} If you ever want to quit, type quit to exit".format(message['CONNECTED']))
                      users_online.connected(message)
                   elif 'JOINED' in message:
                      msg_list.insert(tkinter.END, "{} has joined the chat.".format(message['JOINED']))
                      users_online.joined(message)
                   elif 'DISJOINED' in message:
                      print(message)
                      if 'REASON' in message:
                         msg_list.insert(tkinter.END, "{} has been kicked from the chat.".format(message['DISJOINED']))
                      else:
                         msg_list.insert(tkinter.END, "{} has left the chat.".format(message['DISJOINED']))
                      users_online.disjoined(message)
                   else:
                      print('FAIL: Unknow Message {}'.format(message))
             else:# TEXT Message
                msg_list.insert(tkinter.END, msg)
          except OSError:
             print('Terminate thread echo_data')
             msg_list.insert(tkinter.END, "Connection got closed, for unknown reason, try to reconnect.")
             users_online.disjoined(message)
             connect_button.configure(state=['normal'])
             entry_field.configure(state=['disabled'])
             send_button.configure(state=['disabled'])
             return
    
    def send(event=None):
       try:
           msg = my_msg.get()
           my_msg.set("")
           s.send(bytes(msg, "utf8"))
           if msg == "{quit}":
               s.close()
               top.quit()
       except Exception:
          top.quit()
          pass 
    
    def on_closing(event=None):
       my_msg.set("{quit}")
       send()
    
    def connect():
       port = 4000
       send_button.configure(state=['normal'])
       connect_button.configure(state=['disabled'])
       entry_field.configure(state=['normal'])
       print('Server address:{}'.format(entry_server_address.get()))
       host = entry_server_address.get()
       address = (host,port)
       s.connect(address)
       threading.Thread(target=echo_data, args = (s,)).start()
    
    
    class LabelFrame(tk.LabelFrame):
       
       def __init__(self, parent, text):
           self._width = 100
           self._bg = 'white'
           super().__init__(parent, text=text, width=self._width, background=self._bg)
           self.pack(side=tk.RIGHT, fill=tk.Y)
    
       def joined(self, message):
           global user_online
           print('joined({})'.format(message))
           user_online = tk.Label(self, text=message['JOINED'],bg=self._bg)
           user_online.grid(row=None, column=None)
    
       def connected(self, message):
           print('connected({})'.format(message))
           tk.Label(self, text=message['CONNECTED'], bg=self._bg).grid()
           if 'JOINED' in message:
              for user_name in message['JOINED']:
                 tk.Label(self, text=user_name, bg=self._bg).grid()
    
       def disjoined(self, message):
           print('disjoined({})'.format(message))
           for lbl in self.grid_slaves():
              if lbl['text'] in message.values():
                 lbl.destroy()
    
    
    top = tkinter.Tk()
    top.title("Chat Room")
    messages_frame = tkinter.Frame(top)
    my_msg = tkinter.StringVar()
    my_msg.set("Type your messages here.")
    scrollbar = tkinter.Scrollbar(messages_frame)
    msg_list = tkinter.Listbox(messages_frame, height=15, width=100, yscrollcommand=scrollbar.set)
    scrollbar.pack(side=tkinter.RIGHT, fill=tkinter.Y)
    msg_list.pack(side=tkinter.LEFT, fill=tkinter.BOTH)
    users_online = LabelFrame(messages_frame, 'Users online:')
    messages_frame.pack()
    entry_field = tkinter.Entry(top, textvariable=my_msg)
    entry_field.configure(state='disabled')
    entry_field.bind("<Return>", send)
    entry_field.pack()
    send_button = tkinter.Button(top, text="Send", command=send)
    send_button.configure(state=['disabled'])
    send_button.pack()
    
    le_frame = tkinter.Frame(top)
    le_frame.pack(fill=tkinter.X)
    
    entry_server_address = tkinter.Entry(le_frame)
    tkinter.Label(le_frame, text='Server address:', width=20, anchor='w').pack(side=tkinter.LEFT, padx=5)
    entry_server_address.pack(side=tkinter.LEFT, fill=tkinter.X, expand=True, padx=5)
    connect_button = tkinter.Button(le_frame, text='Connect', command=connect)
    connect_button.pack(side=tkinter.LEFT, padx=5)
    
    top.protocol("WM_DELETE_WINDOW", on_closing)
    
    
    
    tkinter.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

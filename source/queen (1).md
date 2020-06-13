---
title: queen (1)
date: 2020-05-07
---
Example Python program queen (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from urllib import request
* from urllib.error import URLError
* import json
* import tkinter
* import time
* from PIL import ImageTk, Image

## Methods

* def queen():
* def update_clock():
* def resize_image(event):
* def delete_main_input():

## Code

Python tkinter example

    from urllib import request
    from urllib.error import URLError
    import json
    import tkinter
    import time
    from PIL import ImageTk, Image
    
    
    def queen():
        # god_mode_suspended = True
        # if user == 'Admin' and god_mode_suspended != True:
        #     password = input('Password: ')
        #     if password == 'Who will watch the watchers':
        #         print('Administrative mode enabled.')
        #     else:
        #         print('Access Denied.')
        user = input_field.get('1.0', 'end-1c')
        if user == '/options':
            queens_options_window = tkinter.Tk()
            queens_options_window.title('Red Queen v0.4 Options Window')
            queens_options_window.minsize(width=500, height=500)
            input_field.config(state = tkinter.NORMAL)
            input_field.delete(1.0, tkinter.END)
        else :
            try:
                print(user + ' else case ')
                with request.urlopen('https://api.wit.ai/message?v=9.3.2018&q=%s&access_token=Z55PIVTSSFOETKSBPWMNPE6YL6HVK4YP' % request.quote(user)) as wit_api:  # call to wit.ai api
                    wit_api_html = wit_api.read()
                    wit_api_html = wit_api_html.decode()
                    wit_api_data = json.loads(wit_api_html)
                intent = wit_api_data['entities']['Intent'][0]['value']
                term = wit_api_data['entities']['search_term'][0]['value']
                if intent == 'info_on':
                    with request.urlopen('https://kgsearch.googleapis.com/v1/entities:search?query=%s&key=AIzaSyCvgNV4G7mbnu01xai0f0k9NL2ito8vY6s&limit=1&indent=True' % term.replace(' ', '%20')) as response:
                        google_knowledge_base_html = response.read()
                        google_knowledge_base_html = google_knowledge_base_html.decode()
                        google_knowledge_base_data = json.loads(google_knowledge_base_html)
                        print(google_knowledge_base_data['itemListElement'][0]['result']['detailedDescription']['articleBody'])
    
                else:
                    print('Kaje?')
            except URLError:
                error_window = tkinter.Tk()
                error_window.title('Red Queen v0.4 Error Window')
                error_window.minsize(width=500, height=500)
    
    
    def update_clock():
        global time1
        # get the current local time from the PC
        time2 = time.strftime('%H:%M:%S')
        # if time string has changed, update it
        if time2 != time1:
            time1 = time2
            clock.config(text=time2)
            clock.place(x = 810, y = 340)
        # calls itself every 200 milliseconds
        # to update the time display as needed
        # could use >200 ms, but display gets jerky
        clock.after(200, update_clock)
        queen_primary_window.update()
    
    
    def resize_image(event):
        new_width = event.width
        new_height = event.height
        image = copy_of_image.resize((new_width, new_height))
        photo = ImageTk.PhotoImage(image)
        label.config(image=photo)
        label.image = photo  # avoid garbage collection
    
    
    def delete_main_input():
        input_field.delete(1.0, tkinter.END)
    
    
    time1 = ''
    queen_primary_window = tkinter.Tk()
    queen_primary_window.configure(background='#ffffff')
    queen_primary_window.title('The Red Queen v0.4')
    # queen_primary_window.attributes('-fullscreen', True) # TODO : switch to full screen or maximized window
    queen_primary_window.state('zoomed')
    image = Image.open('Laurina Crvena Kraljica.jpg')
    copy_of_image = image.copy()
    photo = ImageTk.PhotoImage(image)
    label = tkinter.Label(queen_primary_window, image=photo)
    label.bind('<Configure>', resize_image)
    label.pack(fill='both', expand='yes')
    input_field_label = tkinter.Label(queen_primary_window, text = 'Enter command : ', background='#FFFFFF')
    input_field_label.place(x = 475, y = 340)
    clock = tkinter.Label(queen_primary_window, font=('times', 12), background='#FCFCFC')
    input_field = tkinter.Text(queen_primary_window, font='Helvetica 20', borderwidth=1, background='#000000', foreground='#FFFFFF', insertbackground='#FFFFFF', blockcursor = True)
    input_field.place(x=(input_field.winfo_screenwidth()/2) - 200, y=(input_field.winfo_screenheight()/2) - 15, height=input_field.winfo_screenheight() / 25, width=input_field.winfo_screenwidth() / 3.5)
    input_field.bind('<Return>', lambda event: queen(), add = '+')
    update_clock()
    queen_primary_window.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

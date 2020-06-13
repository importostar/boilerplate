---
title: omdb_api_tkinter
date: 2020-05-07
---
Example Python program omdb_api_tkinter.py

## Modules

* import tkinter
* from tkinter import ttk
* import requests

## Classes

* class MoviesDB:

## Methods

* def __init__(self, master):
* def createWidgets(self):
* def getMovie(self):
* def clearContents(self):

## Code

Python tkinter example

    import tkinter
    from tkinter import ttk
    import requests
    
    
    class MoviesDB:
    
        def __init__(self, master):
            self.master = master
            self.createWidgets()
    
        def createWidgets(self):
            self.movie_label = ttk.Label(self.master, text='Search for a Movie', background='light blue', font=('helvetica', 20))
            self.movie_label.grid(row=0, sticky='w', padx=50, pady=25)
    
            self.entry = ttk.Entry(self.master, width=50)
            self.entry.grid(row=1, sticky='w', padx=50, pady=5, ipady=3)
    
            self.button = ttk.Button(text='Go', command=self.getMovie)
            self.button.grid(row=2, sticky='w', padx=50, pady=5)
    
            self.movie_frame = ttk.Frame(self.master, width=1000, height=450, relief='groove')
            self.movie_frame.grid_propagate(False)
            self.movie_frame.grid(row=3, sticky='w', padx=50, pady=5)
    
        def getMovie(self):
            if self.movie_frame.grid_slaves():
                self.clearContents()
    
            endpoint = 'http://www.omdbapi.com/'
            payload = {"apikey": "ca9dc15e", "t": self.entry.get()}
            response = requests.get(endpoint, params=payload)
            movie = response.json()
    
            keys = ['Title', 'Year', 'Rated', 'Runtime', 'Genre', 'Director', 'Actors', 'Plot', 'Language', 'Country',
                    'Awards', 'Poster', 'imdbRating']
    
            for item in keys:
                text_val = item + ' : ' + movie[item]
                ttk.Label(self.movie_frame,
                          text=text_val, wraplength=1000,
                          font=('helvetica', 9)).grid(padx=3, pady=3, sticky='w')
    
            self.entry.delete(0, 'end')
    
        def clearContents(self):
                for widget in self.movie_frame.grid_slaves():
                    widget.destroy()
    
    
    
    if __name__ == '__main__':
        master = tkinter.Tk()
        MoviesDB(master)
        master.title('Movies DB')
        master.geometry('1200x650+125+50')
        master.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

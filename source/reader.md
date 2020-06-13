---
title: reader
date: 2020-05-07
---
Example Python program reader.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import os
* import tempfile
* import shutil
* import imghdr
* import webbrowser
* import textwrap
* import tkinter
* from urllib.request import pathname2url
* from tkinter import messagebox, filedialog

## Methods

* def get_images(path):
* def create_html(html_dir):
* def extract_file(compressed_file):

## Code

Python tkinter example

    #!/usr/bin/env python3
    
    import sys
    import os
    import tempfile
    import shutil
    import imghdr
    import webbrowser
    import textwrap
    import tkinter
    
    from urllib.request import pathname2url
    from tkinter import messagebox, filedialog
    
    
    def get_images(path):
        for root, dirs, files in os.walk(path):
            for file in sorted(files):
                fullpath = os.path.join(root, file)
                if imghdr.what(fullpath):
                    yield fullpath
    
    
    def create_html(html_dir):
        html_filename = os.path.join(html_dir, 'index.html')
    
        with open(html_filename, 'w') as html_file:
            html_code = textwrap.dedent(
                    """\
                    <!DOCTYPE html>
                    <html>
                    <head>
                        <title>{title}</title>
                        <style>
                            img {{
                                display: block;
                                margin: 0 auto;
                            }}
                        </style>
                    </head>
                    <body>
                        {images}
                    </body>
                    </html>
                    """.format(
                            title='Longstrip Reader',
                            images=''.join(
                                    '<img src="{}" alt="Couldn\'t load image">'.format(image)
                                    for image in get_images(html_dir))
                    )
            )
    
            print(html_code, file=html_file)
    
        return html_filename
    
    
    def extract_file(compressed_file):
        with tempfile.TemporaryDirectory() as tmp_directory:
            try:
                shutil.unpack_archive(compressed_file, tmp_directory)
    
                html_filename = create_html(tmp_directory)
                webbrowser.open('file:' + pathname2url(html_filename))
    
                messagebox.showinfo('Longstrip Reader', 'Wait for the images to load in your web-browser, then press Ok.')
    
            except shutil.ReadError:
                messagebox.showerror('Longstrip Reader', 'Unknown archive format!\n' + compressed_file)
                sys.exit(1)
    
    
    if __name__ == '__main__':
        filenames = None
        tkinter.Tk().withdraw()
    
        if len(sys.argv) < 2:
             filename = filedialog.askopenfilename(title='Longstrip Reader')
        else:
             filename = sys.argv[1]
    
        if not os.path.isfile(filename):
            messagebox.showerror('Longstrip Reader', 'Wrong filename!\n' + filename)
            sys.exit(1)
        else:
            extract_file(os.path.abspath(filename))
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

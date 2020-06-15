---
title: texttools2
date: 2020-05-07
---
Example Python program texttools2.py

## Modules

* import click
* import textblob
* import sys
* import Tkinter as tk
* import win32clipboard  # will fail if pywin32 isn't installed
* import Tkinter as tk  # if using python < 3.0
* import tkinter as tk  # if using python > 3.0

## Methods

* def read_from_pipeline():
* def split_paragraphs(text):
* def split_sentences(text):
* def split_paragraphs_from_stdin(joinlines):
* def splitsents(joinlines):
* def tkchooselines():
* def buttonclickcommand(index):
* def inner():
* def pyless():
* def get_clipboard_text():

## Code

Python tkinter example

    import click
    import textblob
    
    
    def read_from_pipeline():
        """ Reads data piped through stdin"""
        import sys
        return "".join([line for line in sys.stdin])
    
    
    def split_paragraphs(text):
        paragraphs = [p for p in text.split("\n\n")]
        for p in paragraphs:
            yield p
    
    
    def split_sentences(text):
        """ Generator that yield sentences from a blob of text."""
        tb = textblob.TextBlob(text)
        for sent in tb.sentences:
            yield sent
    
    
    @click.command()
    @click.option("--joinlines", default=True, type=bool,
                  help="Whether to join lines before splitting")
    def split_paragraphs_from_stdin(joinlines):
        """
        ex: type somefile.txt | splitsents
        """
        linesfrompipeline = read_from_pipeline()
        if joinlines:
            text = " ".join(linesfrompipeline)
        else:
            text = '\n'.join(linesfrompipeline)
        for sent in split_sentences(text):
            click.echo(sent)
    
    
    @click.command()
    @click.option("--joinlines", default=True, type=bool,
                  help="Whether to join lines before splitting")
    def splitsents(joinlines):
        """
        ex: type somefile.txt | splitsents
        """
        linesfrompipeline = read_from_pipeline()
        if joinlines:
            text = "".join(linesfrompipeline)
        else:
            text = '\n'.join(linesfrompipeline)
        for sent in split_sentences(text):
            click.echo(sent)
    
    
    @click.command()
    def tkchooselines():
        """ Creates tkinter text widget from lines in stdin with buttons that print to stdout
        """
        import Tkinter as tk
    
        # list of lines from stdin
        linesfrompipeline = read_from_pipeline()
        root = tk.Tk()
        text = tk.Text(root, wrap=tk.NONE)
        text.pack()
    
        buttondict = {}
        for i, line in enumerate(linesfrompipeline):
            buttondict[i] = {}
    
            def buttonclickcommand(index):
                """Factory function that produces statements that print to stdout"""
                memoI = index  # this is a little sketchy since it relies of functional closure to retain the memoized index
    
                def inner():
                    click.echo(buttondict[memoI]['line'])
                    # striketrhough tag assigned when the text is inserted
                    text.tag_config("line{}".format(memoI), overstrike=1)
                    return
                return inner
    
            buttondict[i]['line'] = line.strip()
            buttondict[i]['button'] = tk.Button(
                text, text=str(i), command=buttonclickcommand(i))
            text.window_create(tk.INSERT, window=buttondict[i]['button'])
            text.insert(tk.END, '{}\n'.format(line))
            text.tag_add(
                "line{}".format(i), "{}.1".format(i + 1), "{}.end".format(i + 1))
    
        root.mainloop()
    
    
    @click.command()
    def pyless():
        click.echo_via_pager('\n'.join(('Line %d' % idx for idx in range(200))))
    
    
    @click.command()
    def get_clipboard_text():
        """ Pipes the contents of the clipboard to stdout"""
        try:
            import win32clipboard  # will fail if pywin32 isn't installed
            win32clipboard.OpenClipboard()
            data = win32clipboard.GetClipboardData()
            win32clipboard.CloseClipboard()
            click.echo(data)
        except ImportError:
            try:
                import Tkinter as tk  # if using python < 3.0
            except ImportError:
                import tkinter as tk  # if using python > 3.0
            root = tk.Tk()
            data = root.get_clipboard_text()
            click.echo(data)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

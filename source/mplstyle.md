---
title: mplstyle
date: 2020-05-07
---
Example Python program mplstyle.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from __future__ import print_function
* import matplotlib
* from matplotlib import style as mplstyle
* import os
* import sys
* import shutil
* import argparse
* import requests

## Methods

* def main():
* def get_style_gist(gist_url, style):
* def get_repo_style(user_repo, style):

## Code

Python example

    #!/usr/bin/env python
    # Install a matplotlib style file
    from __future__ import print_function
    import matplotlib
    from matplotlib import style as mplstyle
    import os
    import sys
    import shutil
    import argparse
    import requests
    
    def main():
        parser = argparse.ArgumentParser(description='Install a matplotlib stylesheet')
        parser.add_argument('--gist')
        #parser.add_argument('user_repo', nargs='?', help='GitHub user/repo where style files are hosted')
        parser.add_argument('stylename', help='Style name; appends .mplstyle if not present')
        args = parser.parse_args()
    
        styledir = os.path.join(matplotlib.get_configdir(), 'stylelib')
    
        filepath,ext = os.path.splitext(args.stylename)
        ext = ext or '.mplstyle'
        filename = filepath + ext
    
        if args.gist:
            style = get_style_gist(args.gist, filename)
            outfile = os.path.join(styledir, filename)
            with open(outfile, 'w') as fh:
                fh.write(style)
        else:
            if not os.path.exists(filename):
                print('ERROR: File "%s" does not exist' % filename, file=sys.stderr)
                return 1
            shutil.copy(filename, styledir)
    
        print('Updating style "%s"' % args.stylename)
        mplstyle.reload_library()
    
    
    def get_style_gist(gist_url, style):
        url,id = os.path.split(gist_url)
        print("Reading Gist...")
        r = requests.get('https://api.github.com/gists/' + id)
        if not r.ok:
            print('Error connecting to GitHubi: "%s"' % r.reason)
            sys.exit(1)
        json = r.json()
        files = json['files']
        if style not in files:
            print('Style "%s" not in gist' % style)
            sys.exit(1)
        return files[style]['content']
    
    
    def get_repo_style(user_repo, style):
        url = os.path.join('https://api.github.com/repos/', user_repo, 'contents', style)
        r = requests.get(url)
        if not r.ok:
            print("Error getting %s from GitHub" % style)
            sys.exit(1)
        return r.text
    
    if __name__ == '__main__':
        sys.exit(main())
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

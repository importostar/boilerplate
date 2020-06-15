---
title: _version
date: 2020-05-07
---
Example Python program _version.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import os
* import pickle
* import subprocess
* from datetime import date
* from lxml import html
* import requests

## Methods

* def set_version_tag(version):
* def get_git_revision_short_hash():
* def get_git_commit_short_hash():
* def get_git_user():
* def get_git_user2(user):

## Code

Example Python PyQt program :

    import sys
    import os
    import pickle
    
    __version__ = None
    __version2__ = None
    __releaseDate__ = None
    __releaseDate2__ = None
    __developer__ = None
    __developer2__ = None
    __devhome__ = None
    
    if getattr(sys, "frozen", False):
        # REQ: Travis windows build fails otherwise
        # https://stackoverflow.com/questions/47468705/pyinstaller-could-not-find-or-load-the-qt-platform-plugin-windows
        # https://stackoverflow.com/questions/54132763/how-to-fix-could-not-find-the-qt-platform-plugin-windows-in-when-implemen
        # https://stackoverflow.com/questions/20495620/qt-5-1-1-application-failed-to-start-because-platform-plugin-windows-is-missi
        os.environ["QT_QPA_PLATFORM_PLUGIN_PATH"] = os.path.join(os.getcwd(), "PyQt5", "Qt", "plugins", "platforms", "")
        os.environ["QT_PLUGIN_PATH"] = os.path.join(os.getcwd(), "PyQt5", "Qt", "plugins", "")
        data = None
        if os.path.isfile("version.pckl"):
            data = pickle.load(open("version.pckl", "rb"))
        if data is None:
            sys.stdout.write("\n\nError loading version file\n\n")
        else:
            __version__ = data["version"]
            __version2__ = data["version2"]
            __releaseDate__ = data["r_date"]
            __releaseDate2__ = data["r_date2"]
            __developer__ = data["developer"]
            __developer2__ = data["developer2"]
            __devhome__ = data["devhome"]
    else:
        import subprocess
        from datetime import date
        from lxml import html
        import requests
        args = sys.argv
        tag = True if "--tag" in sys.argv else False
        c_path = os.getcwd()
        p_source = "version.pckl" if c_path.endswith("src") \
            else "src/version.pckl"
    
        def set_version_tag(version):
            c_os = sys.platform
            c_os = "Windows" if c_os.startswith("win") else \
                ("Linux" if c_os.startswith("lin") else "Mac")
            tag = "%s-%s" % (c_os, version)
            print("Setting tag:", tag)
            with open("version.txt", "w") as fh:
                fh.write(tag)
    
        def get_git_revision_short_hash():
            try:
                # ghash = subprocess.check_output(['git',
                #               'rev-parse', '--short', 'HEAD'])
    
                # independent of location as long as there is a git folder
                #   what about if you use setup_user.py install?
                #   what about if you don't have git?
                # can raise a subprocess.CalledProcessError,
                # which means the return code != 0
                ghash = subprocess.check_output(['git', 'describe', '--always'],
                                                cwd=os.getcwd())
    
                ghash = ghash.decode("utf-8").rstrip()
            except:
                # git isn't installed
                ghash = "no.checksum.error"
            return ghash
    
        def get_git_commit_short_hash():
            try:
                c_hash = subprocess.check_output(["git", "rev-parse", "--short", "HEAD"],
                                                 cwd=os.getcwd())
                c_hash = c_hash.decode("utf-8").rstrip()
            except:
                c_hash = "no.checksum.error"
            return c_hash
    
        def get_git_user():
            try:
                c_hash = subprocess.check_output(["git", "config", "user.name"],
                                                 cwd=os.getcwd())
                c_hash = c_hash.decode("utf-8").rstrip()
            except:
                c_hash = "no.checksum.error"
            return c_hash
    
        def get_git_user2(user):
            try:
                if user == "no.checksum.error":
                    raise ValueError
                r = requests.get("https://github.com/%s" % user)
                h_tree = html.fromstring(r.content)
                name = h_tree.xpath("//span[@class='p-name vcard-fullname d-block overflow-hidden']/text()")[0]
                if name == "" or name is None:
                    raise ValueError
            except:
                name = "unknown"
            return name
    
        revision = get_git_revision_short_hash()
        l_commit = get_git_commit_short_hash()
        stage = "-Alpha" if revision.endswith("a") else ("-Beta" if revision.endswith("b") else "")
        today = date.today()
        t_short = today.strftime("%d/%m/%Y")
        t_long = today.strftime("%B %d, %Y")
        __version__ = revision
        __version2__ = '%s%s+%s' % (revision, stage, l_commit)
        __releaseDate__ = t_short
        __releaseDate2__ = t_long
        __developer__ = get_git_user()
        __developer2__ = get_git_user2(__developer__)
        __devhome__ = "https://github.com/%s" % __developer__
        data = {
            "version": __version__,
            "version2": __version2__,
            "r_date": __releaseDate__,
            "r_date2": __releaseDate2__,
            "developer": __developer__,
            "developer2": __developer2__,
            "devhome": __devhome__
        }
        pickle.dump(data, open(p_source, "wb"))
        if tag:
            set_version_tag(__version__)

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

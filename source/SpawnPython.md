---
title: SpawnPython
date: 2020-05-07
---
Example Python program SpawnPython.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import requests
* from zipfile import ZipFile, BadZipFile
* import subprocess
* import os
* import sys
* from distutils.version import StrictVersion
* # Adding "import site" to ._pth file
* f.write("\n# Added by SpawnPython\nimport site\n")
* f.write("import sys\nsys.path.insert(0, \"\")")

## Code

Python example

    import requests
    from zipfile import ZipFile, BadZipFile
    import subprocess
    import os
    import sys
    from distutils.version import StrictVersion
    
    DEFAULT_PYTHON_VERSION = "3.8.1"
    
    # Python version to install
    if len(sys.argv) == 2:
        try:
            python_version_strict = str(StrictVersion(sys.argv[1]))
        except ValueError:
            print("Please provide valid Python version as an argument!")
            sys.exit(1)
        if python_version_strict < StrictVersion("3.6"):
            print("Python version should be higher than 3.6!")
            sys.exit(1)
        python_version = sys.argv[1].strip()
    else:
        python_version = DEFAULT_PYTHON_VERSION
    
    # Python version short (3.8.1 -> 38)
    python_version_short = "".join(python_version.split(".")[:2])
    
    # Python zip
    python_zip_url = "https://www.python.org/ftp/python/" + python_version + "/python-" + python_version + "-embed-amd64.zip"
    python_zip_path = "./python-" + python_version + "-embed-amd64.zip"
    
    # Python folder path
    python_folder_path = "./python-" + python_version
    
    # Python exe path
    python_exe_path = python_folder_path + "/python.exe"
    python_exe_path_win = python_exe_path.replace("/", "\\")
    
    # get_pip.py script
    get_pip_url = "https://bootstrap.pypa.io/get-pip.py"
    get_pip_path = "./get-pip.py"
    get_pip_path_win = get_pip_path.replace("/", "\\")
    
    # pip path
    pip_path = python_folder_path + "/Scripts/pip.exe"
    pip_path_win = pip_path.replace("/", "\\")
    
    print("Downloading, unzipping and installing embeddable Python...")
    
    # Downloading embeddable Python zip archive
    try:
        r = requests.get(python_zip_url)
        r.raise_for_status()
    except requests.exceptions.RequestException as e:
        print("Something went wrong with downloading Python\nYou may have provided non-existent version\nAborting...")
        sys.exit(1)
    
    # Writing embeddable Python zip archive
    try:
        with open(python_zip_path, "wb") as f:
            f.write(r.content)
            f.close()
    except IOError:
        print("Something went wrong with writing ._pth\nAborting...")
        sys.exit(1)
    
    # Unzipping embeddable Python zip archive
    try:
        with ZipFile(python_zip_path, "r") as z:
            z.extractall(python_folder_path)
            z.close()
    except (BadZipFile, IOError):
        print("Something went wrong with unzipping Python zip archive\nAborting...")
        sys.exit(1)
    
    # Removing embeddable Python zip archive
    try:
        os.remove(python_zip_path)
    except OSError:
        print("Something went wrong with deleting Python zip archive\nAborting...")
        sys.exit(1)
    
    # Adding "import site" to ._pth file
    try:
        with open(python_folder_path + "/python" + python_version_short + "._pth", "a") as f:
            f.write("\n# Added by SpawnPython\nimport site\n")
            f.close()
    except IOError:
        print("Something went wrong with writing ._pth\nAborting...")
        sys.exit(1)
    
    # Creating sitecustomize.py
    try:
        with open(python_folder_path + "/sitecustomize.py", "w") as f:
            f.write("import sys\nsys.path.insert(0, \"\")")
            f.close()
    except IOError:
        print("Something went wrong with writing sitecustomize.py\nAborting...")
        sys.exit(1)
    
    # Downloading get_pip.py script
    try:
        r = requests.get(get_pip_url)
    except requests.exceptions.RequestException as e:
        print("Something went wrong with downloading get_pip.py\nAborting...")
        sys.exit(1)
    
    # Writing get_pip.py script
    try:
        with open(get_pip_path, "wb") as f:
            f.write(r.content)
            f.close()
    except IOError:
        print("Something went wrong with writing get_pip.py\nAborting...")
        sys.exit(1)
    
    print("Done!\n\nTrying to install pip...")
    print("\n★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★")
    
    # Running get_pip.py script
    try:
        subprocess.call([python_exe_path_win, get_pip_path_win, "--no-warn-script-location"])
    except OSError:
        print("Something went wrong with running get_pip.py script\nAborting...")
        sys.exit(1)
    
    # Removing get_pip.py script
    try:
        os.remove(get_pip_path)
    except OSError:
        print("Something went wrong with deleting get_pip.py script\n")
        sys.exit(1)
    
    print("★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★★\n")
    print("Done!\nYou can install packages using pip.exe from Scripts directory inside your embeddable Python folder")
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

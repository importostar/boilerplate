---
title: auto_install_aplpy
date: 2020-05-07
---
Example Python program auto_install_aplpy.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import os
* import getopt
* import sys
* import tempfile
* import urllib
* import glob
* import subprocess
* import zipfile
* import tarfile
* import shutil
* import string
* from distutils import version
* imported = __import__(package)
* print " * installed: %s" % find_version(imported)
* if version.LooseVersion(find_version(imported)) < required[package]:

## Classes

* class MissingVersion(Exception):

## Methods

* def help():
* def find_version(module):
* def download_stable(url):
* def download_unstable(protocol, url):

## Code

Python example

    # The purpose of this script is to automatically install APLpy and all
    # the dependencies (except numpy and matplotlib), either using the latest
    # stable versions of packages, or the latest unstable versions from svn or
    # git repositories.
    
    import os
    import getopt
    import sys
    import tempfile
    import urllib
    import glob
    import subprocess
    import zipfile
    import tarfile
    import shutil
    import string
    from distutils import version
    
    
    def help():
        print '''
     The purpose of this script is to automatically install APLpy and all
     the dependencies (except numpy and matplotlib), either using the latest
     stable versions of packages, or the latest unstable versions from svn or
     git repositories. By default, packages are installed only if recent
     versions are not already present. This script can install:
    
       * pyfits (http://www.stsci.edu/resources/software_hardware/pyfits)
       * pywcs (https://trac6.assembla.com/astrolib)
       * pyparsing (http://pyparsing.wikispaces.com/)
       * pyregion (http://leejjoon.github.com/pyregion/)
       * pyavm (https://github.com/astrofrog/pyavm)
       * python-montage (http://astrofrog.github.com/python-montage/).
         Note: this is only the Python wrapper to the Montage mosaicking
         software - the latter needs to be installed separately (see
         http://montage.ipac.caltech.edu/)
       * Python Imaging Library (http://www.pythonware.com/products/pil/)
       * APLpy (http://aplpy.github.com)
    
     and optionally, if the --extra flag is specified:
    
       * ATpy (http://aplpy.github.com)
       * vo (https://trac6.assembla.com/astrolib)
    
     The script cannot install the following APLpy dependencies:
    
       * numpy (http://numpy.scipy.org/)
       * matplotlib (http://matplotlib.sourceforge.net/)
    
     These need to be installed beforehand, and the script will abort if they
     are not.
    
     To do a dry run to check what needs to be installed without installing:
    
       python auto_install_aplpy.py --dry
    
     To install the required dependencies using the latest stable packages:
    
       python auto_install_aplpy.py --stable
    
     To install the latest svn/git versions of these pacakges:
    
       python auto_install_aplpy.py --unstable
    
     To install the extra packages, add --extra to the command, e.g.:
    
       python auto_install_aplpy.py --stable --extra
    
     To force installation of all packages, add --force to the command, e.g.:
    
       python auto_install_aplpy.py --stable --force
    
     To install packages without root permissions, either specify the
     installation prefix with `--prefix=...`, or simply add `--user` (Python 2.6
     or later)
    
     To see this help message:
    
       python auto_install_aplpy.py
          '''
    
    
    try:
        opts, args = getopt.getopt(sys.argv[1:], "suefd", ['unstable', 'stable', 'extra', 'force', 'dry', 'user', 'prefix='])
    except getopt.GetoptError, err:
        help()
        sys.exit(2)
    
    mode = None
    force = False
    install_options = []
    
    noforce = ['numpy', 'matplotlib']
    
    packages = ['numpy', 'matplotlib', 'pyfits', 'pywcs', 'pyparsing', \
                'pyregion', 'pyavm', 'montage', 'Image', 'aplpy']
    
    for i, j in opts:
        if i in ("-u", "--unstable"):
            mode = 'unstable'
        elif i in ("-s", "--stable"):
            mode = 'stable'
        elif i in ("-e", "--extra"):
            packages += ['atpy', 'vo']
        elif i in ("-f", "--force"):
            force = True
        elif i in ("-d", "--dry"):
            mode = 'dry'
        elif i in ("--user"):
            install_options.append("--user")
        elif i in ("--prefix"):
            install_options.append("--prefix=%s" % j)
    
    if mode is None:
        help()
        sys.exit()
    
    required = {}
    required['numpy'] = version.LooseVersion('1.4.1')
    required['matplotlib'] = version.LooseVersion('1.0.0')
    required['pyfits'] = version.LooseVersion('2.4.0')
    required['pywcs'] = version.LooseVersion('1.8')
    required['pyparsing'] = version.LooseVersion('1.5')
    required['pyregion'] = None
    required['pyavm'] = version.LooseVersion('0.1.0')
    required['montage'] = version.LooseVersion('0.9.2')
    required['Image'] = version.LooseVersion('1.1.6')
    required['aplpy'] = version.LooseVersion('0.9.8')
    
    # extra packages
    required['atpy'] = version.LooseVersion('0.9.5.3')
    required['vo'] = version.LooseVersion('0.5')
    
    stable = {}
    stable['numpy'] = None
    stable['matplotlib'] = None
    stable['pyfits'] = 'http://pypi.python.org/packages/source/p/pyfits/pyfits-3.0.6.tar.gz'
    stable['pywcs'] = 'http://stsdas.stsci.edu/astrolib/pywcs-1.10-4.7.tar.gz'
    stable['pyparsing'] = 'http://downloads.sourceforge.net/project/pyparsing/pyparsing/pyparsing-1.5.3/pyparsing-1.5.3.zip'
    stable['pyregion'] = 'http://github.com/downloads/leejjoon/pyregion/pyregion-1.0.tar.gz'
    stable['pyavm'] = 'http://github.com/downloads/astrofrog/pyavm/PyAVM-0.1.4.tar.gz'
    stable['montage'] = 'http://github.com/downloads/astrofrog/python-montage/python-montage-0.9.2.tar.gz'
    stable['Image'] = 'http://effbot.org/downloads/Imaging-1.1.7.tar.gz'
    stable['aplpy'] = 'https://github.com/downloads/aplpy/aplpy/APLpy-0.9.8.tar.gz'
    
    # extra packages
    stable['atpy'] = 'https://github.com/downloads/atpy/atpy/ATpy-0.9.5.3.tar.gz'
    stable['vo'] = 'http://stsdas.stsci.edu/astrolib/vo-0.7.2.tar.gz'
    
    unstable = {}
    unstable['numpy'] = None
    unstable['matplotlib'] = None
    unstable['pyfits'] = ('svn', 'http://svn6.assembla.com/svn/pyfits/trunk/')
    unstable['pywcs'] = ('svn', 'http://svn6.assembla.com/svn/astrolib/trunk/pywcs')
    unstable['pyparsing'] = ('svn', 'https://pyparsing.svn.sourceforge.net/svnroot/pyparsing/src')
    unstable['pyregion'] = ('git', 'http://github.com/leejjoon/pyregion.git')
    unstable['pyavm'] = ('git', 'git://github.com/astrofrog/pyavm.git')
    unstable['montage'] = ('git', 'http://github.com/astrofrog/python-montage.git')
    unstable['Image'] = None
    unstable['aplpy'] = ('git', 'git://github.com/aplpy/aplpy.git')
    
    # extra packages
    unstable['atpy'] = ('git', 'git://github.com/atpy/atpy.git')
    unstable['vo'] = ('svn', 'http://svn6.assembla.com/svn/astrolib/trunk/vo')
    
    
    logfile = open('install.log', 'wb')
    
    
    class MissingVersion(Exception):
        pass
    
    
    def find_version(module):
        if hasattr(module, '__version__'):
            return module.__version__
        elif hasattr(module, 'VERSION'):
            return module.VERSION
        else:
            raise MissingVersion("No version information")
    
    
    def download_stable(url):
    
        filename = os.path.basename(url)
        print " - Downloading"
        urllib.urlretrieve(url, filename)
        print " - Expanding"
        if filename.endswith('.zip'):
            z = zipfile.ZipFile(filename, 'r')
            z.extractall()
        elif filename.endswith('.tar.gz'):
            t = tarfile.open(filename, 'r:gz')
            t.extractall()
        else:
            raise Exception("Unknown file extension: %s" % filename)
    
        os.remove(filename)
    
    
    def download_unstable(protocol, url):
    
        print " - Checking out latest developer version"
    
        if protocol == 'svn':
            os.system("svn --non-interactive --trust-server-cert co %s >& /dev/null" % url)
        elif protocol == 'git':
            os.system("git clone %s >& /dev/null" % url)
        else:
            raise Exception("Unknown protocol: %s" % protocol)
    
    
    for package in packages:
    
        print "-"*50
        print "Package: %s" % package
    
        try:
    
            imported = __import__(package)
    
            if required[package] is not None:
                print " * installed: %s" % find_version(imported)
                print " * required: %s" % required[package].vstring
                if version.LooseVersion(find_version(imported)) < required[package]:
                    print " - Installed version is out of date, updating"
                    install = True
                else:
                    install = False
            else:
                print " * installed"
                install = False
    
        except MissingVersion:
    
            print " * installed: cannot determine version"
            if required[package] is not None:
                print " * required: %s" % required[package].vstring
    
            install = True
    
        except ImportError:
    
            print " * installed: none"
            if required[package] is not None:
                print " * required: %s" % required[package].vstring
    
            install = True
    
        if mode != 'dry' and (install or (force and not package in noforce)):
    
            start_dir = os.path.abspath('.')
    
            try:
    
                temp_dir = tempfile.mkdtemp()
                os.chdir(temp_dir)
    
                if mode == 'stable':
    
                    print " - Installing %s" % package
    
                    if stable[package] is None:
                        print "ERROR: This package cannot be installed by this script."
                        print "       Please install it manually before proceeding."
                        sys.exit()
    
                    download_stable(stable[package])
    
                else:
    
                    print " - Installing %s" % package
    
                    if unstable[package] is None:
                        if stable[package] is not None:
                            download_stable(stable[package])
                        else:
                            print "ERROR: This package cannot be installed by this script."
                            print "       Please install it manually before proceeding."
                            sys.exit()
                    else:
                        download_unstable(*unstable[package])
    
                files = glob.glob(os.path.join('.', '*'))
    
                if len(files) == 0:
                    raise Exception("No files in archive")
                elif len(files) > 1:
                    raise Exception("Too many files in archive")
                else:
                    os.chdir(files[0])
                    print " - Building"
                    p = subprocess.Popen(['python', 'setup.py', 'install'] + install_options, stderr=logfile, stdout=logfile)
                    sts = os.waitpid(p.pid, 0)[1]
                    if sts == 0:
                        print " - Installed!"
                    else:
                        print " - An error occured. Please check the install.log file"
    
            finally:
                os.chdir(start_dir)
                shutil.rmtree(temp_dir)
    
        elif mode == 'dry':
            if install:
                print " - Install: yes"
            else:
                print " - Install: no"
    
    print "-"*50
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

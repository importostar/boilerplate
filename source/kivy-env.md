---
title: kivy env
date: 2020-05-07
---
Example Python program kivy-env.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from __future__ import print_function
* import subprocess
* import sys
* import os
* from os import makedirs, listdir, remove, rename
* from os.path import exists, join, abspath, isdir, isfile, splitext
* import argparse
* from subprocess import Popen, PIPE
* from shutil import rmtree, copytree, copy2
* from glob import glob
* import hashlib
* import re
* from zipfile import ZipFile
* from urllib.request import urlretrieve
* from urllib import urlretrieve

## Classes

* class WindowsPortablePythonBuild(object):

## Methods

* def report_hook(block_count, block_size, total_size):
* def exec_binary(status, cmd, env=None, cwd=None, shell=True):
* def parse_args(self):
* parser.add_argument("--gendef", help='Path to the gendef executable '
* self.gendef = join(abspath(gendef), 'gendef.exe')
* def run(self):
* def get_python(self, width, build_path, url, md5):
* def patch_python_x64(self, pydir, env, pyver):
* pydef = join(libs, py + '.def')
* def get_pip_deps(self, pydir, env, pywin, pygame):
* def get_glew(self, pydir, mingw, glew, arch, env):
* glew_def = join(libs, 'glew32.def')

## Code

Python tkinter example

    from __future__ import print_function
    import subprocess
    import sys
    import os
    from os import makedirs, listdir, remove, rename
    from os.path import exists, join, abspath, isdir, isfile, splitext
    import argparse
    from subprocess import Popen, PIPE
    from shutil import rmtree, copytree, copy2
    from glob import glob
    import hashlib
    import re
    from zipfile import ZipFile
    try:
        from urllib.request import urlretrieve
    except ImportError:
        from urllib import urlretrieve
    
    
    def report_hook(block_count, block_size, total_size):
        p = block_count * block_size * (100.0 / total_size if total_size else 1)
        print("\b\b\b\b\b\b\b\b\b", "%06.2f%%" % p, end=' ')
    
    
    def exec_binary(status, cmd, env=None, cwd=None, shell=True):
        print(status)
        print(' '.join(cmd))
        proc = Popen(cmd, stdout=PIPE, stderr=PIPE, env=env, cwd=cwd, shell=shell)
        a, b = proc.communicate()
        print(a, end='')
        print(b, end='')
    
    
    class WindowsPortablePythonBuild(object):
        '''Custom build command that builds portable win32 python
        and kivy deps.
        '''
    
        pydb = {
            'py2.7.8_x86': ('https://www.python.org/ftp/python/2.7.8/python-2.7.8.msi',
                            'ef95d83ace85d1577b915dbd481977d4'),
            'py2.7.8_x64': ('https://www.python.org/ftp/python/2.7.8/python-2.7.8.amd64.msi',
                            '38cadfcac6dd56ecf772f2f3f14ee846'),
            'py3.4.1_x86': ('https://www.python.org/ftp/python/3.4.1/python-3.4.1.msi',
                            '4940c3fad01ffa2ca7f9cc43a005b89a'),
            'py3.4.1_x64': ('https://www.python.org/ftp/python/3.4.1/python-3.4.1.amd64.msi',
                            '25440653f27ee1597fd6b3e15eee155f'),
            'py2.7.6_x86': ('https://www.python.org/ftp/python/2.7.6/python-2.7.6.msi',
                            'ac54e14f7ba180253b9bae6635d822ea')}
    
        pip_deps = ['cython', 'docutils', 'pygments', 'requests', 'plyer',
                    'kivy-garden', 'wheel']
    
        pywin_baseurl = ''
        pygame_baseurl = ''
    
        dist_dir = None
        temp_dir = ''
        build_pythons = []
        mingw = ''
        mingw64 = ''
        noclean = False
        gendef = ''
    
        def parse_args(self):
            parser = argparse.ArgumentParser(description='Generates portable package'
                ' for usage with kivy. It includes python and MinGW for 64 and 32 bit '
                'platforms. To use, you specify the python versions to build, paths '
                'to MinGW, a path to local copies of pygame binaries, and '
                'the path to gendef if building 64 bit.')
            parser.add_argument("--dir", help='path of dist directory to use '
                'for building the portable python, the end result will be output '
                'to this directory. Defaults to cwd.', default=os.getcwd())
            parser.add_argument("pythons", help='The '
            'pythons to generate, in the format of `pyversion_arch`, where version'
            ' is e.g. 2.7.6 and arch is either  x86 or x64. For example: '
            'py2.7.8_x86.')
            parser.add_argument("mingw", help='Path to MinGW. '
                'To get it, download mingw-get-setup.exe from '
                'http://sourceforge.net/projects/mingw/files/Installer/mingw-get-setup.exe/download.'
                '\nTo install, create a directory and run the installer which will install'
                'a command line or gui mingw package manager. Then you install the required'
                'packages (gcc-core) using that manager. Pass the name of this '
                'directory to this option.')
            parser.add_argument("mingw64", help='Path to 64 bit MinGW. '
                'To get it, download the latest 64 bit mingw from '
                'http://sourceforge.net/projects/mingw-w64/files/Toolchains%%20targetting%%20Win64/Personal%%20Builds/mingw-builds/.'
                '\nTo install, just unzip the downloaded file to a directory and pass the name of'
                'that directory to this option.')
            parser.add_argument("--pywin", help='Initial path of the pywin '
                'binaries url on sourceforge. Defaults to '
                'http://iweb.dl.sourceforge.net/project/pywin32/pywin32/Build%20219/',
                default='http://iweb.dl.sourceforge.net/project/pywin32/pywin32/Build%20219/')
            parser.add_argument("pygame", help='Path to pygame binaries downloaded '
                'from http://www.lfd.uci.edu/~gohlke/pythonlibs/#pygame')
            parser.add_argument("--gendef", help='Path to the gendef executable '
                'you can get it from http://sourceforge.net/projects/mingw/files/MinGW/Extension/gendef/gendef-1.0.1346/'
                'This path should have a file called gendef.exe. If not specified'
                " it's assumed to be in MinGW/bin.", default='')
            parser.add_argument("--noclean", help='Whether to remove the python '
                'and MinGW build if it already exists', action="store_true")
    
            args = parser.parse_args()
            self.dist_dir = base = abspath(args.dir)
            self.temp_dir = join(base, 'temp')
    
            pydb = self.pydb
            build_py = []
            for py in args.pythons.split(','):
                py = py.strip()
                if py not in pydb:
                    raise Exception('Python {} not recognized'.format(py))
                build_py.append((py, pydb[py]))
            self.build_pythons = build_py
    
            self.mingw = abspath(args.mingw)
            self.mingw64 = abspath(args.mingw64)
            self.pywin_baseurl = args.pywin
            self.pygame_path = args.pygame
            self.noclean = args.noclean
            gendef = args.gendef
            if gendef:
                self.gendef = join(abspath(gendef), 'gendef.exe')
            else:
                self.gendef = 'gendef.exe'
    
        def run(self):
            self.parse_args()
            width = self.width = 30
    
            print("-" * width)
            print("Generating python distribution")
            print("-" * width)
            print("\nPreparing Build...")
            print("-" * width)
            dist_dir = self.dist_dir
            print('Working in {}'.format(dist_dir))
    
            temp = self.temp_dir
            if exists(temp):
                print("*Removing old temp dir, {}".format(temp))
                rmtree(temp, ignore_errors=True)
            print('Creating temp directory {}'.format(temp))
            makedirs(temp)
    
            py_pat = re.compile('py([0-9])\.([0-9])\.([0-9])_x([0-9]+)')
    
            for pyname, (url, md5) in self.build_pythons:
                print('\n')
                print("-" * width)
                print("Preparing python {}".format(pyname))
                print("-" * width)
                name = pyname.replace('.', '')
                build_path = join(dist_dir, name)
                m = re.match(py_pat, pyname)
                pyver = m.groups()[:3]
                arch = int(m.group(4))
                patch_py = False
                pydir = join(build_path, 'Python')
    
                if not self.noclean and exists(build_path):
                    print("*Cleaning old build dir, {}".format(build_path))
                    rmtree(build_path, ignore_errors=True)
                if not exists(build_path):
                    print("*Creating build directory: {}".format(build_path))
                    makedirs(build_path)
                if not exists(pydir):
                    self.get_python(width, build_path, url, md5)
                    patch_py = arch == 64
    
                mingw = join(build_path, 'MinGW')
                if not exists(mingw):
                    src = self.mingw if arch == 86 else self.mingw64
                    print('Copying Mingw from {} to {}'.format(src, mingw))
                    copytree(src, mingw)
    
                env = os.environ.copy()
                env['PATH'] = '{};{};{};{}'.format(pydir, join(mingw, 'bin'),
                    join(pydir, 'Scripts'), env['PATH'])
                env['PYTHONPATH'] = ''
    
                if patch_py:
                    print('Patching python')
                    self.patch_python_x64(pydir, env, pyver)
    
                if arch == 86:
                    pywin = 'pywin32-219.win32-py{}.{}.exe'.format(*pyver[:2])
                    pygame = 'pygame-1.9.2a0.win32-py{}.{}.exe'.format(*pyver[:2])
                    glew = 'glew-1.5.7-win32.zip'
                else:
                    pywin = 'pywin32-219.win-amd64-py{}.{}.exe'.format(*pyver[:2])
                    pygame = 'pygame-1.9.2a0.win-amd64-py{}.{}.exe'.format(*pyver[:2])
                    glew = 'glew-1.5.7-win64.zip'
    
                self.get_glew(pydir, mingw, glew, arch, env)
    
                self.get_pip_deps(pydir, env, self.pywin_baseurl + pywin,
                                  join(self.pygame_path, pygame))
    
            print('Removing temp directory')
            rmtree(temp, ignore_errors=True)
            print('Done')
    
        def get_python(self, width, build_path, url, md5):
            print("*Downloading: {}".format(url))
            print("Progress: 000.00%", end=' ')
            f, _ = urlretrieve(url, join(self.temp_dir, url.split('/')[-1]),
                               reporthook=report_hook)
            print(" [Done]")
    
            print("Verifying MD5", end=' ')
            with open(f, 'rb') as fd:
                md5_read = hashlib.md5(fd.read()).hexdigest()
                if md5_read != md5:
                    raise Exception('MD5 not verified. Gotten: {}, expected: {}'.
                                    format(md5_read, md5))
            print(" Done")
    
            pydir = join(build_path, 'Python')
            makedirs(pydir)
            exec_binary("*Extracting python to {}".format(pydir),
                        ['msiexec', '/a', f, '/qb', 'TARGETDIR={}'.format(pydir)],
                        shell=False)
            print("\nCleaning python")
            print("-" * width)
    
            for f in listdir(pydir):
                if f.endswith('.msi'):
                    f = join(pydir, f)
                    print('Removing {}'.format(f))
                    remove(f)
                    break
    
            for d in ('tcl', 'Doc', join('Lib', 'test'), join('Lib', 'lib-tk'),
                      join('Lib', 'idlelib')):
                print('Removing {}'.format(d))
                rmtree(join(pydir, d), ignore_errors=True)
    
            ignore_list = ()
            for f in listdir(join(pydir, 'Lib')):
                if f in ignore_list:
                    continue
                f = join(pydir, 'Lib', f)
                if not isdir(f):
                    continue
    
                dirs = os.listdir(f)
                if 'test' in dirs and isdir(join(f, 'test')):
                    f = join(f, 'test')
                elif 'tests' in dirs and isdir(join(f, 'tests')):
                    f = join(f, 'tests')
                else:
                    continue
                print('Removing {}'.format(f))
                rmtree(f, ignore_errors=True)
    
            for f in listdir(join(pydir, 'DLLs')):
                if (f.startswith('tcl') or f.startswith('tk') or
                    f.startswith('_tkinter')):
                    f = join(pydir, 'DLLs', f)
                    print('Removing {}'.format(f))
                    remove(f)
    
            f = join(pydir, 'Lib', 'distutils', 'distutils.cfg')
            print('Writing {}'.format(f))
            with open(f, 'w') as fd:
                fd.write('[build]\ncompiler=mingw32\n')
            makedirs(join(pydir, 'Scripts'))
    
        def patch_python_x64(self, pydir, env, pyver):
            gendef = self.gendef
    
            libs = join(pydir, 'libs')
            py = 'python{}{}'.format(*pyver[:2])
            pylib = py + '.lib'
            pydll = join(pydir, py + '.dll')
            pydef = join(libs, py + '.def')
    
            # see http://bugs.python.org/issue4709 and
            # http://ascend4.org/Setting_up_a_MinGW-w64_build_environment
            rename(join(libs, pylib), join(libs, 'old_' + pylib))
            exec_binary('Gendefing ' + pydll, [gendef, pydll], env, libs)
            exec_binary('Generating libpython.a',
                        ['dlltool', '--dllname', pydll, '--def', pydef,
                         '--output-lib', 'lib' + py + '.a'], env, libs, shell=True)
            remove(pydef)
    
            print('Getting python pyconfig.h patch')
            url = 'http://bugs.python.org/file12411/mingw-w64.patch'
            include = join(pydir, 'include')
            patch_name = url.split('/')[-1]
            patch, _ = urlretrieve(url, join(include, patch_name))
            exec_binary('Patching {}\\pyconfig.h'.format(include),
                        ['git', 'apply', patch_name], env, include, shell=True)
            remove(patch)
    
            # see http://bugs.python.org/issue16472
            print('Patching cygwinccompiler.py')
            cyg = join(pydir, 'Lib', 'distutils', 'cygwinccompiler.py')
            with open(cyg) as fd:
                lines = fd.readlines()
    
            with open(cyg, 'w') as fd:
                for line in lines:
                    if line == '        self.dll_libraries = get_msvcr()\n':
                        fd.write('        #self.dll_libraries = get_msvcr()\n')
                    else:
                        fd.write(line)
    
        def get_pip_deps(self, pydir, env, pywin, pygame):
            width = self.width
            temp_dir = self.temp_dir
            py = join(pydir, 'python.exe')
    
            print('Getting pip and easy install')
            url = 'https://bootstrap.pypa.io/get-pip.py'
            pip, _ = urlretrieve(url, join(temp_dir, url.split('/')[-1]))
            url = 'https://bootstrap.pypa.io/ez_setup.py'
            ez, _ = urlretrieve(url, join(temp_dir, url.split('/')[-1]))
    
            exec_binary('Installing pip', [py, pip], env, pydir, shell=True)
            exec_binary('Installing easy install', [py, ez], env, pydir, shell=True)
    
            pip = join(pydir, 'Scripts', 'pip.exe')
            for mod in self.pip_deps:
                exec_binary('Installing {}'.format(mod), [pip, 'install', mod],
                            env, pydir, shell=True)
    
            wheel = join(pydir, 'Scripts', 'wheel.exe')
    
            print("Downloading pywin32. Progress: 000.00%", end=' ')
            pywin, _ = urlretrieve(pywin, join(temp_dir, pywin.split('/')[-1]),
                                   reporthook=report_hook)
            print(' [Done]')
    
            a = listdir(temp_dir)
            exec_binary('Converting {} to wheel'.format(pywin),
                        [wheel, 'convert', pywin], env, temp_dir, shell=True)
            b = listdir(temp_dir)
            exec_binary('Converting {} to wheel'.format(pygame),
                        [wheel, 'convert', pygame], env, temp_dir, shell=True)
            # get the path of the wheel file generated
            pywin = join(temp_dir, list(set(b) - set(a))[0])
            pygame = join(temp_dir, list(set(listdir(temp_dir)) - set(b))[0])
    
            exec_binary('Installing the wheel {}'.format(pywin),
                        [wheel, 'install', '--force', pywin], env, pydir, shell=True)
            exec_binary('Installing the wheel {}'.format(pygame),
                        [wheel, 'install', pygame], env, pydir, shell=True)
    
        def get_glew(self, pydir, mingw, glew, arch, env):
            temp_dir = self.temp_dir
            url = 'http://iweb.dl.sourceforge.net/project/glew/glew/1.5.7/' + glew
    
            print("*Getting glew. Downloading: {}".format(url))
            print("Progress: 000.00%", end=' ')
            f, _ = urlretrieve(url, join(temp_dir, glew), reporthook=report_hook)
            print(" [Done]")
    
            z = join(temp_dir, splitext(glew)[0])
            print('Extracting glew {}'.format(f))
            with open(f, 'rb') as fd:
                ZipFile(fd).extractall(z)
            z = join(z, 'glew-1.5.7')
    
            print('Distributing glew to mingw and python')
            include = join(mingw, 'include', 'GL')
            py_include = join(pydir, 'include', 'GL')
            if not exists(include):
                makedirs(include)
            makedirs(py_include)
            for f in glob(join(z, 'include', 'GL', '*')):
                try:
                    copy2(f, include)
                except:
                    pass
                copy2(f, py_include)
    
            lib = join(mingw, 'lib')
            copy2(join(z, 'bin', 'glew32.dll'), pydir)
            try:
                copy2(join(z, 'bin', 'glew32.dll'), lib)
                copy2(join(z, 'lib', 'glew32.lib'), lib)
                copy2(join(z, 'lib', 'glew32s.lib'), lib)
            except:
                pass
    
            gendef = self.gendef
            libs = join(pydir, 'libs')
            glew_dll = join(z, 'bin', 'glew32.dll')
            glew_def = join(libs, 'glew32.def')
    
            exec_binary('Gendefing ' + glew_dll, [gendef, glew_dll], env, libs)
            exec_binary('Generating libglew32.a',
                        ['dlltool', '--dllname', glew_dll, '--def', glew_def,
                         '--output-lib', 'libglew32.a'], env, libs)
            remove(glew_def)
    
    
    if __name__ == '__main__':
        WindowsPortablePythonBuild().run()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

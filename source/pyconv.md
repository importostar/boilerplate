---
title: pyconv
date: 2020-05-07
---
Example Python program pyconv.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import re
* import sys

## Classes

* class SpecPyGeneric:

## Methods

* def __init__(self):
* def read_spec(self):
* def write_spec(self):
* def add_macros(self):
* def handle_requires(self):

## Code

Python example

    import re
    import sys
    
    filename = sys.argv[1]
    
    macro_section="""# Macros for py2/py3 compatibility
    %if 0%{?fedora} || 0%{?rhel} > 7
    %global pyver %{python3_pkgversion}
    %else
    %global pyver 2
    %endif
    
    %global pyver_bin python%{pyver}
    %global pyver_sitelib %python%{pyver}_sitelib
    %global pyver_install %py%{pyver}_install
    %global pyver_build %py%{pyver}_build
    # End of macros for py2/py3 compatibility"""
    
    macro_list=macro_section.split('\n')
    
    class SpecPyGeneric:
        def __init__(self):
            self.req_excepts = []
            self.br_excepts = []
    
        def read_spec(self):
            """ Read Spec as list """
            with open(filename) as infile:
                self.data = infile.read().split('\n')
    
        def write_spec(self):
            with open('temp.spec', 'w') as outfile:
                for i in self.data:
                    outfile.write(i+'\n')
        def add_macros(self):
            if "%global pyver %{python3_pkgversion}" not in self.data:
                self.data = macro_list + self.data
        def handle_requires(self):
            for index, line in enumerate(self.data):
                if "Requires" in line:
                    self.data[index] = line.replace("python2-", "python%{pyver}-")
                    if re.match("^Requires.*python-", line):
                        self.req_excepts.append(line)
                    if re.match("^BuildRequires.*python-", line):
                        self.br_excepts.append(line)
                 
                elif "%package -n" in line:
                    self.data[index] = line.replace("python-", "python%{pyver}-")
                    pprovide = self.data[index].split('-n')[1].strip()
                    data = '%{?python_provide:%python_provide ' + pprovide + '}'
                    self.data.insert(index+2, data)
                elif "%files -n" in line:
                    self.data[index] = line.replace("python-", "python%{pyver}-")
                elif "%description -n" in line:
                    self.data[index] = line.replace("python-", "python%{pyver}-")
                elif "python2_sitelib" in line:
                    self.data[index] = line.replace("python2_sitelib", "pyver_sitelib")
                elif "sphinx-build" in line:
                    self.data[index] = line.replace("sphinx-build", "sphinx-build-%{pyver}")
                elif "oslo-config-generator" in line:
                    self.data[index] = line.replace("oslo-config-generator", "oslo-config-generator-%{pyver}")
                elif re.search(".*python.*setup.py.*install", line):
                    self.data[index] = "%{pyver_install}"
                elif re.search(".*python.*setup.py build", line):
                    self.data[index] = "%{pyver_build}"
                elif "%{__python2}" in line:
                    self.data[index] = line.replace("%{__python2}", "%{pyver_bin}")
    
            if len(self.req_excepts) > 0:
                print('# Handle python2 exception\n%if %{pyver} == 2')
                for i in self.req_excepts:
                    print(i)
                print('%else')
                for i in self.req_excepts:
                    print(i.replace("python-", "python%{pyver}-"))
                print('%endif')
    
            if len(self.br_excepts) > 0:
                print('# Handle python2 exception\n%if %{pyver} == 2')
                for i in self.br_excepts:
                    print(i)
                print('%else')
                for i in self.br_excepts:
                    print(i.replace("python-", "python%{pyver}-"))
                print('%endif')
                
            
    if __name__ == '__main__':
        obj = SpecPyGeneric()
        obj.read_spec()
        obj.handle_requires()
        obj.add_macros()
        obj.write_spec()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

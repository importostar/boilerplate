---
title: conan_python_package_tools
date: 2020-05-07
---
Example Python program conan_python_package_tools.py

## Modules

* import os
* import subprocess
* from conans import tools
* from conans.errors import ConanException
* 'from distutils.sysconfig import get_python_lib; print get_python_lib(1)'
* 'from distutils.sysconfig import get_python_lib; print get_python_lib()'

## Methods

* def python_path(_conanfile):
* def build(conanfile):
* def package(conanfile):

## Code

Python example

    import os
    import subprocess
    
    from conans import tools
    from conans.errors import ConanException
    
    
    def python_path(_conanfile):
        """Return path to python interpreter for which package is being built"""
        return "python"
    
    
    def build(conanfile):
        """Build pyton package from source"""
    
        archive_path = os.path.join(conanfile.source_folder,
                                    conanfile.ARCHIVE_NAME)
    
        if not os.path.exists(archive_path):
            raise ConanException(
                ("Source package is not found at path: {}.\n"
                 "Please make sure that you ran conan export / conan upload"))
    
        conanfile.output.info("Unpacking archive {} to build folder...".format(
            conanfile.ARCHIVE_NAME))
        tools.unzip(archive_path)
    
        setup_cfg_path = os.path.join(conanfile.FOLDER_NAME, "setup.cfg")
        conanfile.output.info(
            "Patching {} to disable automated download...".format(setup_cfg_path))
        tools.save(
            setup_cfg_path, ("[easy_install]\n"
                             "allow_hosts = None\n"),
            append=True)
    
        build_command = "{} setup.py install -O1 --root={}".format(
            python_path(conanfile), conanfile.build_folder)
        conanfile.output.info(
            "Building package with command: {}".format(build_command))
        with tools.chdir(conanfile.FOLDER_NAME):
            conanfile.run(build_command)
    
    
    def package(conanfile):
        """Copy built python package into conan cache directory"""
    
        python = python_path(conanfile)
    
        python_sitearch = subprocess.check_output([
            python, "-c",
            'from distutils.sysconfig import get_python_lib; print get_python_lib(1)'
        ]).decode().strip()[1:]
    
        conanfile.output.info(
            "Platform-dependent modules are installed into: {}".format(
                python_sitearch))
    
        python_sitelib = subprocess.check_output([
            python, "-c",
            'from distutils.sysconfig import get_python_lib; print get_python_lib()'
        ]).decode().strip()[1:]
    
        conanfile.output.info(
            "Pure python modules are installed into: {}".format(python_sitelib))
    
        conanfile.copy("*", src=python_sitearch)
        conanfile.copy("*", src=python_sitelib)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

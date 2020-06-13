---
title: numpyxc
date: 2020-05-07
---
Example Python program numpyxc.py

## Modules

* import os
* from setup import setup_package
* from numpy.distutils import fcompiler, ccompiler
* from numpy.distutils.intelccompiler import IntelCCompiler
* # Export it into a module that is __import__ed by np.distutils.ccompiler
* import sys, imp
* # import os
* # from distutils import sysconfig
* # import numpy.core.setup as core_setup

## Classes

* class IntelMICCompiler(IntelCCompiler):
* # print ccompiler.compiler_class # {name: (module_name, module_member_name, desc), ...}
* # print fcompiler.fcompiler_class # {name: (name, klass, desc), ...}

## Methods

*   def __init__ (self, verbose=0, dry_run=0, force=0):
* #   def get_python_lib(plat_specific=0, standard_lib=0, prefix=None):
* #   def get_python_inc(plat_specific=0, prefix=None):

## Code

Python example

    import os
    
    xcprefix = os.environ.get('PYTHONXCPREFIX', None)
    if not xcprefix:
      raise Exception("Must specify PYTHONXCPREFIX as an argument to make this work")
    
    from setup import setup_package
    
    from numpy.distutils import fcompiler, ccompiler
    from numpy.distutils.intelccompiler import IntelCCompiler
    
    class IntelMICCompiler(IntelCCompiler):
      """ A modified Intel compiler compatible with an gcc built Python."""
      compiler_type = 'intelmic'
      cc_exe = 'icc'
    
      def __init__ (self, verbose=0, dry_run=0, force=0):
        IntelCCompiler.__init__ (self, verbose, dry_run, force)
        compiler = "icc -mmic -fPIC -I{0}/include -L{0}/lib -L{0}/lib/python2.7".format(xcprefix)
        self.set_executables(compiler=compiler + ' -shared',
                             compiler_so=compiler,
                             compiler_cxx=compiler,
                             linker_exe=compiler,
                             linker_so=compiler + ' -shared')
    
    # Export it into a module that is __import__ed by np.distutils.ccompiler
    import sys, imp
    imc = imp.new_module('numpy.distutils.intelmiccompiler')
    sys.modules['numpy.distutils.intelmiccompiler'] = imc
    imc.IntelMICCompiler = IntelMICCompiler
    
    # print ccompiler.compiler_class # {name: (module_name, module_member_name, desc), ...}
    ccompiler.compiler_class['intelmic'] = ('intelmiccompiler', 'IntelMICCompiler', 'Intel Compiler for Xeon Phi')
    
    fcompiler.load_all_fcompiler_classes()
    # print fcompiler.fcompiler_class # {name: (name, klass, desc), ...}
    
    # The following taken from https://bitbucket.org/lambacck/distutilscross
    # import os
    # from distutils import sysconfig
    # xcprefix = os.environ.get('PYTHONXCPREFIX', None)
    # if xcprefix:
    #   _get_python_lib = sysconfig.get_python_lib
    #   def get_python_lib(plat_specific=0, standard_lib=0, prefix=None):
    #     return _get_python_lib(plat_specific, standard_lib, xcprefix)
    #   sysconfig.get_python_lib = get_python_lib
    
    #   _get_python_inc = sysconfig.get_python_inc
    #   def get_python_inc(plat_specific=0, prefix=None):
    #     return _get_python_inc(plat_specific, xcprefix)
    #   sysconfig.get_python_inc = get_python_inc
    
    #   sysconfig.PREFIX = xcprefix
    #   sysconfig.EXEC_PREFIX = xcprefix
    #   # now force a reload from the given prefix
    #   sysconfig._config_vars = None
    #   print sysconfig.get_config_var("LDSHARED")
    
    # Disable SSE intrinsics since they don't seem to work
    
    # import numpy.core.setup as core_setup
    # setup_common.OPTIONAL_HEADERS = []
    # setup_common.OPTIONAL_INTRINSICS = [] # TODO: reintroduce other builtins
    
    setup_package()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

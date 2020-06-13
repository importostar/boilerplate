---
title: cpython (1)
date: 2020-05-07
---
Example Python program cpython (1).py

## Modules

* # http://mathamy.com/import-accio-bootstrapping-python-grammar.html
* https://chrisyeh96.github.io/2017/08/08/definitive-guide-python-imports.html

## Code

Python example

    # cpython internals
    # https://leanpub.com/insidethepythonvirtualmachine/read#leanpub-auto-compiling-python-source-code
    # https://hackernoon.com/modifying-the-python-language-in-7-minutes-b94b0a99ce14
    # http://mathamy.com/import-accio-bootstrapping-python-grammar.html
    # https://realpython.com/cpython-source-code-guide/
    
    
    
    object.__call__(self[, args...])
    Called when the instance is “called” as a function; if this method is defined, x(arg1, arg2, ...) is a shorthand for x.__call__(arg1, arg2, ...).
    # https://docs.python.org/3/reference/datamodel.html#object.__call__
    
    
    http://jakevdp.github.io/blog/2014/05/09/why-python-is-slow/
    http://foobarnbaz.com/2012/07/08/understanding-python-variables/
        
    https://towardsdatascience.com/assignment-shallow-or-deep-a-story-about-pythons-memory-management-b8fad87bfa6c
    https://chrisyeh96.github.io/2017/08/08/definitive-guide-python-imports.html
    
    # cpython entrance
    #The three source files you need to inspect to see this process are:
        Programs/python.c is a simple entry point.
        Modules/main.c contains the code to bring together the whole process, loading configuration, executing code and clearing up memory.
        Python/initconfig.c loads the configuration from the system environment and merges it with any command-line flags.
    # https://realpython.com/cpython-source-code-guide/
        
    #Initializing and finalizing the interpreter
    #https://docs.python.org/3/c-api/init.html
    void Py_Initialize()
    #Initialize the Python interpreter. In an application embedding Python, this should be called before using any other Python/C API functions; see Before Python Initialization for the few exceptions.
    #This initializes the table of loaded modules (sys.modules), and creates the fundamental modules builtins, __main__ and sys. It also initializes the module search path (sys.path). It does not set sys.argv; use PySys_SetArgvEx() for that. This is a no-op when called for a second time (without calling Py_FinalizeEx() first). There is no return value; it is a fatal error if the initialization fails.
    #Note On Windows, changes the console mode from O_TEXT to O_BINARY, which will also affect non-Python uses of the console using the C Runtime.
    
    
    static int
    pymain_main(_PyArgv *args)
    =>
        static PyStatus
        pymain_init(const _PyArgv *args)
        =>
            static PyStatus
            init_interp_main(PyThreadState *tstate)
            =>
                static PyStatus
                pyinit_main(PyThreadState *tstate)
                =>
                    static PyStatus
                    init_interp_main(PyThreadState *tstate)
                    =>
                        status = init_sys_streams(tstate);
                        if (_PyStatus_EXCEPTION(status)) {
                            return status;
                        }
    
                        status = init_set_builtins_open();
                        if (_PyStatus_EXCEPTION(status)) {
                            return status;
                        }
    
                        status = add_main_module(interp);
                        if (_PyStatus_EXCEPTION(status)) {
                            return status;
                        }
                  
    # python builtins
    # https://www.tutorialsteacher.com/python/python-builtin-modules
    # https://www.tutorialspoint.com/built-in-objects-in-python-builtins
    
    # python scope
    https://www.geeksforgeeks.org/scope-resolution-in-python-legb-rule/
        
    # books:
    # https://docs.python-guide.org/intro/learning/
    
    # design
    # https://github.com/hblanks/zen-of-python-by-example
        

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

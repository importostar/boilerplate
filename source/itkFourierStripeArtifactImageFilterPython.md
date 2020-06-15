---
title: itkFourierStripeArtifactImageFilterPython
date: 2020-05-07
---
Example Python program itkFourierStripeArtifactImageFilterPython.py

## Modules

* from sys import version_info as _swig_python_version_info
* from new import instancemethod as new_instancemethod
* def swig_import_helper():
* import importlib
* return importlib.import_module(mname)
* return importlib.import_module('_itkFourierStripeArtifactImageFilterPython')
* _itkFourierStripeArtifactImageFilterPython = swig_import_helper()
* del swig_import_helper
* def swig_import_helper():
* from os.path import dirname
* import imp
* import _itkFourierStripeArtifactImageFilterPython
* _itkFourierStripeArtifactImageFilterPython = swig_import_helper()
* del swig_import_helper
* import _itkFourierStripeArtifactImageFilterPython
* import builtins as __builtin__
* import __builtin__
* import itkImageRegionPython
* import itkIndexPython
* import itkOffsetPython
* import itkSizePython
* import pyBasePython
* import ITKCommonBasePython
* import itkImageToImageFilterAPython
* import itkImagePython
* import stdcomplexPython
* import itkCovariantVectorPython
* import itkVectorPython
* import vnl_vectorPython
* import vnl_matrixPython
* import vnl_vector_refPython
* import itkFixedArrayPython
* import itkRGBPixelPython
* import itkMatrixPython
* import vnl_matrix_fixedPython
* import itkPointPython
* import itkSymmetricSecondRankTensorPython
* import itkRGBAPixelPython
* import itkImageSourcePython
* import itkImageSourceCommonPython
* import itkVectorImagePython
* import itkVariableLengthVectorPython
* import itkImageToImageFilterCommonPython
* import itkTemplate
* import itkTemplate

## Classes

* class itkFourierStripeArtifactImageFilterIF2(itkImageToImageFilterAPython.itkImageToImageFilterIF2IF2):
* class itkFourierStripeArtifactImageFilterIF3(itkImageToImageFilterAPython.itkImageToImageFilterIF3IF3):

## Methods

* def swig_import_helper():
* def swig_import_helper():
* def _swig_setattr_nondynamic(self, class_type, name, value, static=1):
* def _swig_setattr(self, class_type, name, value):
* def _swig_getattr(self, class_type, name):
* def _swig_repr(self):
* def _swig_setattr_nondynamic_method(set):
* def set_attr(self, name, value):
* def itkFourierStripeArtifactImageFilterIF3_New():
* def itkFourierStripeArtifactImageFilterIF2_New():
* def __init__(self, *args, **kwargs):
* def __New_orig__():
* def Clone(self):
* def SetDirection(self, _arg):
* def GetDirection(self):
* def SetSigma(self, _arg):
* def GetSigma(self):
* def SetStartFrequency(self, _arg):
* def GetStartFrequency(self):
* def cast(obj):
* def GetPointer(self):
* def New(*args, **kargs):
* def itkFourierStripeArtifactImageFilterIF2___New_orig__():
* def itkFourierStripeArtifactImageFilterIF2_cast(obj):
* def __init__(self, *args, **kwargs):
* def __New_orig__():
* def Clone(self):
* def SetDirection(self, _arg):
* def GetDirection(self):
* def SetSigma(self, _arg):
* def GetSigma(self):
* def SetStartFrequency(self, _arg):
* def GetStartFrequency(self):
* def cast(obj):
* def GetPointer(self):
* def New(*args, **kargs):
* def itkFourierStripeArtifactImageFilterIF3___New_orig__():
* def itkFourierStripeArtifactImageFilterIF3_cast(obj):

## Code

Python example

    # This file was automatically generated by SWIG (http://www.swig.org).
    # Version 3.0.12
    #
    # Do not make changes to this file unless you know what you are doing--modify
    # the SWIG interface file instead.
    
    from sys import version_info as _swig_python_version_info
    if _swig_python_version_info >= (3, 0, 0):
        new_instancemethod = lambda func, inst, cls: _itkFourierStripeArtifactImageFilterPython.SWIG_PyInstanceMethod_New(func)
    else:
        from new import instancemethod as new_instancemethod
    if _swig_python_version_info >= (2, 7, 0):
        def swig_import_helper():
            import importlib
            pkg = __name__.rpartition('.')[0]
            mname = '.'.join((pkg, '_itkFourierStripeArtifactImageFilterPython')).lstrip('.')
            try:
                return importlib.import_module(mname)
            except ImportError:
                return importlib.import_module('_itkFourierStripeArtifactImageFilterPython')
        _itkFourierStripeArtifactImageFilterPython = swig_import_helper()
        del swig_import_helper
    elif _swig_python_version_info >= (2, 6, 0):
        def swig_import_helper():
            from os.path import dirname
            import imp
            fp = None
            try:
                fp, pathname, description = imp.find_module('_itkFourierStripeArtifactImageFilterPython', [dirname(__file__)])
            except ImportError:
                import _itkFourierStripeArtifactImageFilterPython
                return _itkFourierStripeArtifactImageFilterPython
            try:
                _mod = imp.load_module('_itkFourierStripeArtifactImageFilterPython', fp, pathname, description)
            finally:
                if fp is not None:
                    fp.close()
            return _mod
        _itkFourierStripeArtifactImageFilterPython = swig_import_helper()
        del swig_import_helper
    else:
        import _itkFourierStripeArtifactImageFilterPython
    del _swig_python_version_info
    
    try:
        _swig_property = property
    except NameError:
        pass  # Python < 2.2 doesn't have 'property'.
    
    try:
        import builtins as __builtin__
    except ImportError:
        import __builtin__
    
    def _swig_setattr_nondynamic(self, class_type, name, value, static=1):
        if (name == "thisown"):
            return self.this.own(value)
        if (name == "this"):
            if type(value).__name__ == 'SwigPyObject':
                self.__dict__[name] = value
                return
        method = class_type.__swig_setmethods__.get(name, None)
        if method:
            return method(self, value)
        if (not static):
            object.__setattr__(self, name, value)
        else:
            raise AttributeError("You cannot add attributes to %s" % self)
    
    
    def _swig_setattr(self, class_type, name, value):
        return _swig_setattr_nondynamic(self, class_type, name, value, 0)
    
    
    def _swig_getattr(self, class_type, name):
        if (name == "thisown"):
            return self.this.own()
        method = class_type.__swig_getmethods__.get(name, None)
        if method:
            return method(self)
        raise AttributeError("'%s' object has no attribute '%s'" % (class_type.__name__, name))
    
    
    def _swig_repr(self):
        try:
            strthis = "proxy of " + self.this.__repr__()
        except __builtin__.Exception:
            strthis = ""
        return "<%s.%s; %s >" % (self.__class__.__module__, self.__class__.__name__, strthis,)
    
    
    def _swig_setattr_nondynamic_method(set):
        def set_attr(self, name, value):
            if (name == "thisown"):
                return self.this.own(value)
            if hasattr(self, name) or (name == "this"):
                set(self, name, value)
            else:
                raise AttributeError("You cannot add attributes to %s" % self)
        return set_attr
    
    
    import itkImageRegionPython
    import itkIndexPython
    import itkOffsetPython
    import itkSizePython
    import pyBasePython
    import ITKCommonBasePython
    import itkImageToImageFilterAPython
    import itkImagePython
    import stdcomplexPython
    import itkCovariantVectorPython
    import itkVectorPython
    import vnl_vectorPython
    import vnl_matrixPython
    import vnl_vector_refPython
    import itkFixedArrayPython
    import itkRGBPixelPython
    import itkMatrixPython
    import vnl_matrix_fixedPython
    import itkPointPython
    import itkSymmetricSecondRankTensorPython
    import itkRGBAPixelPython
    import itkImageSourcePython
    import itkImageSourceCommonPython
    import itkVectorImagePython
    import itkVariableLengthVectorPython
    import itkImageToImageFilterCommonPython
    
    def itkFourierStripeArtifactImageFilterIF3_New():
      return itkFourierStripeArtifactImageFilterIF3.New()
    
    
    def itkFourierStripeArtifactImageFilterIF2_New():
      return itkFourierStripeArtifactImageFilterIF2.New()
    
    class itkFourierStripeArtifactImageFilterIF2(itkImageToImageFilterAPython.itkImageToImageFilterIF2IF2):
        """Proxy of C++ itkFourierStripeArtifactImageFilterIF2 class."""
    
        thisown = _swig_property(lambda x: x.this.own(), lambda x, v: x.this.own(v), doc='The membership flag')
    
        def __init__(self, *args, **kwargs):
            raise AttributeError("No constructor defined")
        __repr__ = _swig_repr
    
        def __New_orig__():
            """__New_orig__() -> itkFourierStripeArtifactImageFilterIF2_Pointer"""
            return _itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF2___New_orig__()
    
        __New_orig__ = staticmethod(__New_orig__)
    
        def Clone(self):
            """Clone(itkFourierStripeArtifactImageFilterIF2 self) -> itkFourierStripeArtifactImageFilterIF2_Pointer"""
            return _itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF2_Clone(self)
    
    
        def SetDirection(self, _arg):
            """SetDirection(itkFourierStripeArtifactImageFilterIF2 self, unsigned int const _arg)"""
            return _itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF2_SetDirection(self, _arg)
    
    
        def GetDirection(self):
            """GetDirection(itkFourierStripeArtifactImageFilterIF2 self) -> unsigned int"""
            return _itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF2_GetDirection(self)
    
    
        def SetSigma(self, _arg):
            """SetSigma(itkFourierStripeArtifactImageFilterIF2 self, double const _arg)"""
            return _itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF2_SetSigma(self, _arg)
    
    
        def GetSigma(self):
            """GetSigma(itkFourierStripeArtifactImageFilterIF2 self) -> double"""
            return _itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF2_GetSigma(self)
    
    
        def SetStartFrequency(self, _arg):
            """SetStartFrequency(itkFourierStripeArtifactImageFilterIF2 self, double const _arg)"""
            return _itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF2_SetStartFrequency(self, _arg)
    
    
        def GetStartFrequency(self):
            """GetStartFrequency(itkFourierStripeArtifactImageFilterIF2 self) -> double"""
            return _itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF2_GetStartFrequency(self)
    
        __swig_destroy__ = _itkFourierStripeArtifactImageFilterPython.delete_itkFourierStripeArtifactImageFilterIF2
    
        def cast(obj):
            """cast(itkLightObject obj) -> itkFourierStripeArtifactImageFilterIF2"""
            return _itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF2_cast(obj)
    
        cast = staticmethod(cast)
    
        def GetPointer(self):
            """GetPointer(itkFourierStripeArtifactImageFilterIF2 self) -> itkFourierStripeArtifactImageFilterIF2"""
            return _itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF2_GetPointer(self)
    
    
        def New(*args, **kargs):
            """New() -> itkFourierStripeArtifactImageFilterIF2
    
            Create a new object of the class itkFourierStripeArtifactImageFilterIF2 and set the input and the parameters if some
            named or non-named arguments are passed to that method.
    
            New() tries to assign all the non named parameters to the input of the new objects - the
            first non named parameter in the first input, etc.
    
            The named parameters are used by calling the method with the same name prefixed by 'Set'.
    
            Ex:
    
              itkFourierStripeArtifactImageFilterIF2.New( reader, Threshold=10 )
    
            is (most of the time) equivalent to:
    
              obj = itkFourierStripeArtifactImageFilterIF2.New()
              obj.SetInput( 0, reader.GetOutput() )
              obj.SetThreshold( 10 )
            """
            obj = itkFourierStripeArtifactImageFilterIF2.__New_orig__()
            import itkTemplate
            itkTemplate.New(obj, *args, **kargs)
            return obj
        New = staticmethod(New)
    
    itkFourierStripeArtifactImageFilterIF2.Clone = new_instancemethod(_itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF2_Clone, None, itkFourierStripeArtifactImageFilterIF2)
    itkFourierStripeArtifactImageFilterIF2.SetDirection = new_instancemethod(_itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF2_SetDirection, None, itkFourierStripeArtifactImageFilterIF2)
    itkFourierStripeArtifactImageFilterIF2.GetDirection = new_instancemethod(_itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF2_GetDirection, None, itkFourierStripeArtifactImageFilterIF2)
    itkFourierStripeArtifactImageFilterIF2.SetSigma = new_instancemethod(_itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF2_SetSigma, None, itkFourierStripeArtifactImageFilterIF2)
    itkFourierStripeArtifactImageFilterIF2.GetSigma = new_instancemethod(_itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF2_GetSigma, None, itkFourierStripeArtifactImageFilterIF2)
    itkFourierStripeArtifactImageFilterIF2.SetStartFrequency = new_instancemethod(_itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF2_SetStartFrequency, None, itkFourierStripeArtifactImageFilterIF2)
    itkFourierStripeArtifactImageFilterIF2.GetStartFrequency = new_instancemethod(_itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF2_GetStartFrequency, None, itkFourierStripeArtifactImageFilterIF2)
    itkFourierStripeArtifactImageFilterIF2.GetPointer = new_instancemethod(_itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF2_GetPointer, None, itkFourierStripeArtifactImageFilterIF2)
    itkFourierStripeArtifactImageFilterIF2_swigregister = _itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF2_swigregister
    itkFourierStripeArtifactImageFilterIF2_swigregister(itkFourierStripeArtifactImageFilterIF2)
    
    def itkFourierStripeArtifactImageFilterIF2___New_orig__():
        """itkFourierStripeArtifactImageFilterIF2___New_orig__() -> itkFourierStripeArtifactImageFilterIF2_Pointer"""
        return _itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF2___New_orig__()
    
    def itkFourierStripeArtifactImageFilterIF2_cast(obj):
        """itkFourierStripeArtifactImageFilterIF2_cast(itkLightObject obj) -> itkFourierStripeArtifactImageFilterIF2"""
        return _itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF2_cast(obj)
    
    class itkFourierStripeArtifactImageFilterIF3(itkImageToImageFilterAPython.itkImageToImageFilterIF3IF3):
        """Proxy of C++ itkFourierStripeArtifactImageFilterIF3 class."""
    
        thisown = _swig_property(lambda x: x.this.own(), lambda x, v: x.this.own(v), doc='The membership flag')
    
        def __init__(self, *args, **kwargs):
            raise AttributeError("No constructor defined")
        __repr__ = _swig_repr
    
        def __New_orig__():
            """__New_orig__() -> itkFourierStripeArtifactImageFilterIF3_Pointer"""
            return _itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF3___New_orig__()
    
        __New_orig__ = staticmethod(__New_orig__)
    
        def Clone(self):
            """Clone(itkFourierStripeArtifactImageFilterIF3 self) -> itkFourierStripeArtifactImageFilterIF3_Pointer"""
            return _itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF3_Clone(self)
    
    
        def SetDirection(self, _arg):
            """SetDirection(itkFourierStripeArtifactImageFilterIF3 self, unsigned int const _arg)"""
            return _itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF3_SetDirection(self, _arg)
    
    
        def GetDirection(self):
            """GetDirection(itkFourierStripeArtifactImageFilterIF3 self) -> unsigned int"""
            return _itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF3_GetDirection(self)
    
    
        def SetSigma(self, _arg):
            """SetSigma(itkFourierStripeArtifactImageFilterIF3 self, double const _arg)"""
            return _itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF3_SetSigma(self, _arg)
    
    
        def GetSigma(self):
            """GetSigma(itkFourierStripeArtifactImageFilterIF3 self) -> double"""
            return _itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF3_GetSigma(self)
    
    
        def SetStartFrequency(self, _arg):
            """SetStartFrequency(itkFourierStripeArtifactImageFilterIF3 self, double const _arg)"""
            return _itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF3_SetStartFrequency(self, _arg)
    
    
        def GetStartFrequency(self):
            """GetStartFrequency(itkFourierStripeArtifactImageFilterIF3 self) -> double"""
            return _itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF3_GetStartFrequency(self)
    
        __swig_destroy__ = _itkFourierStripeArtifactImageFilterPython.delete_itkFourierStripeArtifactImageFilterIF3
    
        def cast(obj):
            """cast(itkLightObject obj) -> itkFourierStripeArtifactImageFilterIF3"""
            return _itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF3_cast(obj)
    
        cast = staticmethod(cast)
    
        def GetPointer(self):
            """GetPointer(itkFourierStripeArtifactImageFilterIF3 self) -> itkFourierStripeArtifactImageFilterIF3"""
            return _itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF3_GetPointer(self)
    
    
        def New(*args, **kargs):
            """New() -> itkFourierStripeArtifactImageFilterIF3
    
            Create a new object of the class itkFourierStripeArtifactImageFilterIF3 and set the input and the parameters if some
            named or non-named arguments are passed to that method.
    
            New() tries to assign all the non named parameters to the input of the new objects - the
            first non named parameter in the first input, etc.
    
            The named parameters are used by calling the method with the same name prefixed by 'Set'.
    
            Ex:
    
              itkFourierStripeArtifactImageFilterIF3.New( reader, Threshold=10 )
    
            is (most of the time) equivalent to:
    
              obj = itkFourierStripeArtifactImageFilterIF3.New()
              obj.SetInput( 0, reader.GetOutput() )
              obj.SetThreshold( 10 )
            """
            obj = itkFourierStripeArtifactImageFilterIF3.__New_orig__()
            import itkTemplate
            itkTemplate.New(obj, *args, **kargs)
            return obj
        New = staticmethod(New)
    
    itkFourierStripeArtifactImageFilterIF3.Clone = new_instancemethod(_itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF3_Clone, None, itkFourierStripeArtifactImageFilterIF3)
    itkFourierStripeArtifactImageFilterIF3.SetDirection = new_instancemethod(_itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF3_SetDirection, None, itkFourierStripeArtifactImageFilterIF3)
    itkFourierStripeArtifactImageFilterIF3.GetDirection = new_instancemethod(_itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF3_GetDirection, None, itkFourierStripeArtifactImageFilterIF3)
    itkFourierStripeArtifactImageFilterIF3.SetSigma = new_instancemethod(_itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF3_SetSigma, None, itkFourierStripeArtifactImageFilterIF3)
    itkFourierStripeArtifactImageFilterIF3.GetSigma = new_instancemethod(_itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF3_GetSigma, None, itkFourierStripeArtifactImageFilterIF3)
    itkFourierStripeArtifactImageFilterIF3.SetStartFrequency = new_instancemethod(_itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF3_SetStartFrequency, None, itkFourierStripeArtifactImageFilterIF3)
    itkFourierStripeArtifactImageFilterIF3.GetStartFrequency = new_instancemethod(_itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF3_GetStartFrequency, None, itkFourierStripeArtifactImageFilterIF3)
    itkFourierStripeArtifactImageFilterIF3.GetPointer = new_instancemethod(_itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF3_GetPointer, None, itkFourierStripeArtifactImageFilterIF3)
    itkFourierStripeArtifactImageFilterIF3_swigregister = _itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF3_swigregister
    itkFourierStripeArtifactImageFilterIF3_swigregister(itkFourierStripeArtifactImageFilterIF3)
    
    def itkFourierStripeArtifactImageFilterIF3___New_orig__():
        """itkFourierStripeArtifactImageFilterIF3___New_orig__() -> itkFourierStripeArtifactImageFilterIF3_Pointer"""
        return _itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF3___New_orig__()
    
    def itkFourierStripeArtifactImageFilterIF3_cast(obj):
        """itkFourierStripeArtifactImageFilterIF3_cast(itkLightObject obj) -> itkFourierStripeArtifactImageFilterIF3"""
        return _itkFourierStripeArtifactImageFilterPython.itkFourierStripeArtifactImageFilterIF3_cast(obj)
    
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
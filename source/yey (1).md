---
title: yey (1)
date: 2020-05-07
---
Example Python program yey (1).py

## Modules

* from ctypes import c_ssize_t, c_void_p, c_int, c_void_p, create_string_buffer, cast, WINFUNCTYPE, CFUNCTYPE, windll, cdll, CDLL
* from PyQt5.QtCore import Qt, QTimer, QObject
* from PyQt5.QtGui import QResizeEvent, QFocusEvent
* from PyQt5.QtWidgets import QWidget, QDialog, QDialogButtonBox, QPushButton, qApp
* import os
* import sys
* import idaapi
* import idc

## Classes

* class TemporaryFilter(QObject):
* class NativeHook:

## Methods

* def _ida_lib_path(ea):
* def _ida_lib():
* def _query(window, predicate):
* def _recursive(widget):
* def __init__(self, filepath):
* def eventFilter(self, obj, event):
* def ask_file_handler(self):
* def __init__(self, **kwargs):
* def handler(self, user_data, code, va_args):
* def __enter__(self):
* def __exit__(self, *args):
* def load_clr_file(filepath):

## Code

Example Python PyQt program :

    from ctypes import c_ssize_t, c_void_p, c_int, c_void_p, create_string_buffer, cast, WINFUNCTYPE, CFUNCTYPE, windll, cdll, CDLL
    from PyQt5.QtCore import Qt, QTimer, QObject
    from PyQt5.QtGui import QResizeEvent, QFocusEvent
    from PyQt5.QtWidgets import QWidget, QDialog, QDialogButtonBox, QPushButton, qApp
    
    import os
    import sys
    import idaapi
    import idc
    
    IDADIR = idaapi.idadir('')
    
    
    def _ida_lib_path(ea):
        ea_name = 'ida64' if idc.__EA64__ else 'ida'
        if sys.platform == 'win':
            path = os.path.join(IDADIR, ea_name + ".dll")
        elif sys.platform == 'darwin':
            path = os.path.join(IDADIR, "lib" + ea_name + ".dylib")
        else:
            path = os.path.join(IDADIR, "lib" + ea_name + ".so")
        return os.path.normpath(path)
    
    
    def _ida_lib():
        ea_name = 'ida64' if idc.__EA64__ else 'ida'
        if sys.platform == 'win32':
            functype = WINFUNCTYPE
            lib = getattr(windll, ea_name)
        elif sys.platform == 'darwin':
            functype = CFUNCTYPE
            lib = CDLL(_ida_lib_path(64 if idc.__EA64__ else 32))
        else:
            functype = CFUNCTYPE
            lib = getattr(cdll, 'lib' + ea_name)
        return functype, lib
    
    
    functype, lib = _ida_lib()
    hook_cb_t = functype(c_void_p, c_void_p, c_int, c_void_p)
    
    hooker = lib.hook_to_notification_point
    hooker.argtypes = [c_int, hook_cb_t, c_void_p]
    
    unhooker = lib.unhook_from_notification_point
    unhooker.argtypes = [c_int, hook_cb_t, c_void_p]
    
    
    def _query(window, predicate):
        results = []
    
        def _recursive(widget):
            for item in widget.children():
                if not isinstance(item, QWidget):
                    continue
                if predicate(item):
                    results.append(item)
                _recursive(item)
        _recursive(window)
        return results
    
    
    class TemporaryFilter(QObject):
        def __init__(self, filepath):
            super(TemporaryFilter, self).__init__()
            filepath = os.path.abspath(filepath)
            assert os.path.isfile(filepath)
    
            self.filepath = filepath
    
        def eventFilter(self, obj, event):
            is_colors_dialog = lambda: isinstance(obj, QDialog) and 'IDA Colors' in obj.windowTitle()
            if isinstance(event, QResizeEvent) and is_colors_dialog():
                obj.setWindowFlags(Qt.Window | Qt.FramelessWindowHint)
                obj.setFixedSize(0, 0)
                obj.setGeometry(0, 0, 0, 0)
                event.accept()
                return 1
            if isinstance(event, QFocusEvent) and is_colors_dialog():
                qApp.removeEventFilter(self)
                buttons = [widget for widget in obj.children() if isinstance(
                    widget, QDialogButtonBox)][0]
                button = buttons.buttons()[-4]
    
                with NativeHook(ask_file=self.ask_file_handler):
                    button.click()
    
                QTimer.singleShot(0, lambda: obj.accept())
                return 1
            return 0
    
        def ask_file_handler(self):
            return create_string_buffer(self.filepath)
    
    
    class NativeHook:
        NAMES = {
            'ask_file': 0x1d
        }
    
        def __init__(self, **kwargs):
            self.hooks = {NativeHook.NAMES[key]
                : value for key, value in kwargs.items()}
            self._handler = hook_cb_t(self.handler)
    
        def handler(self, user_data, code, va_args):
            if code in self.hooks:
                try:
                    res = self.hooks[code]()
                    return cast(res, c_void_p).value
                except:
                    return 0
            else:
                return 0
    
        def __enter__(self):
            hooker(1, self._handler, None)
    
        def __exit__(self, *args):
            unhooker(1, self._handler, None)
    
    
    def load_clr_file(filepath):
        eventFilter = TemporaryFilter(filepath)
        qApp.installEventFilter(eventFilter)
    
        return idaapi.process_ui_action('SetColors')
    
    
    load_clr_file('C:/Users/berry/Downloads/ida-consonance.clr.txt')
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

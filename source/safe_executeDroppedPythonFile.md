---
title: safe_executeDroppedPythonFile
date: 2020-05-07
---
Example Python program safe_executeDroppedPythonFile.py

## Modules

* import safe_executeDroppedPythonFile
* import sys
* from os.path import splitext as _splitext
* import maya.cmds as cmds
* import imp
* from imp import load_module
* import maya.app.general.executeDroppedPythonFile as module

## Methods

* def applyModestPatch():
* def executeDroppedPythonFile(*args):
* def applyOverridePatch():
* def executeDroppedPythonFile(droppedFile, obj):
* def _getOrigModule():
* def _cleanModules(name):

## Code

Python example

    # -*- coding: utf-8 -*-
    u"""
    maya.app.general.executeDroppedPythonFile を少しは安全にするパッチ。
    
    元の実装を尊重したラッパー `applyModestPatch` か
    実装を丸ごと上書きする `applyOverridePatch` のどちらか好きな方を実行するとパッチが適用される。
    どちらとも繰り返し実行しても副作用はないので、切り替えも可能。
    元の実装の function は同モジュールの _executeDroppedPythonFile 属性に退避される。
    
    使用例::
        import safe_executeDroppedPythonFile
        safe_executeDroppedPythonFile.applyOverridePatch()
    """
    import sys
    from os.path import splitext as _splitext
    
    
    def applyModestPatch():
        u"""
        ごく最低限なラッパーに置き換えるパッチ。
    
        - ドロップしたスクリプトがエラーを起こしても sys.path 先頭にゴミが残らないようにする。
        - ドロップしたスクリプトが sys.modules に残らないようにする。
        """
        module = _getOrigModule()
        origFunc = module._executeDroppedPythonFile
    
        def executeDroppedPythonFile(*args):
            try:
                origFunc(*args)
            except:
                sys.path.pop(0)
                raise
            finally:
                _cleanModules(_splitext(args[0])[0])
    
        module.executeDroppedPythonFile = executeDroppedPythonFile
    
    
    def applyOverridePatch():
        u"""
        実装を丸ごと置き換えるパッチ。
    
        - 実行にあたって、そもそも sys.path 先頭にパスを追加しない。
        - ドロップしたスクリプトが sys.modules に残らないようにする。
        - 関数 onMayaDroppedPythonFile が無くても警告を出さない。
        """
        import maya.cmds as cmds
        import imp
        from imp import load_module
        descDict = dict([(d[0], d) for d in imp.get_suffixes()])
        module = _getOrigModule()
    
        def executeDroppedPythonFile(droppedFile, obj):
            theModuleName, suffix = _splitext(droppedFile)
            desc = descDict.get(suffix)
            if not desc:
                return False
    
            fp = open(droppedFile, desc[1])
            if fp:
                try:
                    try:
                        loadedModule = load_module(theModuleName, fp, droppedFile, desc)
                    finally:
                        fp.close()
                    func = getattr(loadedModule, 'onMayaDroppedPythonFile', None)
                    if func:
                        return func(obj)
                finally:
                    _cleanModules(theModuleName)
            return False
    
        module.executeDroppedPythonFile = executeDroppedPythonFile
    
    
    def _getOrigModule():
        import maya.app.general.executeDroppedPythonFile as module
        if not hasattr(module, '_executeDroppedPythonFile'):
            module._executeDroppedPythonFile = module.executeDroppedPythonFile
        return module
    
    
    def _cleanModules(name):
        sys.modules.pop(name, None)
        name += '.'
        for x in list(sys.modules):
            if x.startswith(name):
                del sys.modules[x]
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

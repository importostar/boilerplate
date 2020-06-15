---
title: external_src
date: 2020-05-07
---
Example Python program external_src.py

## Modules

* from PyQt5 import QtCore

## Methods

* def qInitResources():
* def qCleanupResources():

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    # Resource object code
    #
    # Created by: The Resource Compiler for PyQt5 (Qt v5.10.1)
    #
    # WARNING! All changes made in this file will be lost!
    
    from PyQt5 import QtCore
    
    qt_resource_data = b"\
    \x00\x00\x00\x2a\
    \x54\
    \x68\x69\x73\x20\x69\x73\x20\x74\x68\x65\x20\x63\x6f\x6e\x74\x65\
    \x6e\x74\x73\x20\x6f\x66\x20\x65\x78\x74\x65\x72\x6e\x61\x6c\x5f\
    \x73\x72\x63\x20\x66\x69\x6c\x65\x2e\
    "
    
    qt_resource_name = b"\
    \x00\x0c\
    \x0a\x21\x33\xa3\
    \x00\x65\
    \x00\x78\x00\x74\x00\x65\x00\x72\x00\x6e\x00\x61\x00\x6c\x00\x5f\x00\x73\x00\x72\x00\x63\
    "
    
    qt_resource_struct_v1 = b"\
    \x00\x00\x00\x00\x00\x02\x00\x00\x00\x01\x00\x00\x00\x01\
    \x00\x00\x00\x00\x00\x00\x00\x00\x00\x01\x00\x00\x00\x00\
    "
    
    qt_resource_struct_v2 = b"\
    \x00\x00\x00\x00\x00\x02\x00\x00\x00\x01\x00\x00\x00\x01\
    \x00\x00\x00\x00\x00\x00\x00\x00\
    \x00\x00\x00\x00\x00\x00\x00\x00\x00\x01\x00\x00\x00\x00\
    \x00\x00\x01\x64\x4b\x72\x26\xa2\
    "
    
    qt_version = QtCore.qVersion().split('.')
    if qt_version < ['5', '8', '0']:
        rcc_version = 1
        qt_resource_struct = qt_resource_struct_v1
    else:
        rcc_version = 2
        qt_resource_struct = qt_resource_struct_v2
    
    def qInitResources():
        QtCore.qRegisterResourceData(rcc_version, qt_resource_struct, qt_resource_name, qt_resource_data)
    
    def qCleanupResources():
        QtCore.qUnregisterResourceData(rcc_version, qt_resource_struct, qt_resource_name, qt_resource_data)
    
    qInitResources()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

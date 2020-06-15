---
title: qmlcomponent_obj_ownership
date: 2020-05-07
---
Example Python program qmlcomponent_obj_ownership.py
This program creates a PyQt GUI

## Modules

* import sys
* import textwrap
* import sip
* from PyQt5.QtQml import QQmlEngine, QQmlComponent
* from PyQt5.QtWidgets import QApplication
* from PyQt5.QtCore import QUrl
* import QtQuick 2.0

## Methods

* def main():

## Code

Example Python PyQt program :

    import sys
    import textwrap
    
    import sip
    
    from PyQt5.QtQml import QQmlEngine, QQmlComponent
    from PyQt5.QtWidgets import QApplication
    from PyQt5.QtCore import QUrl
    
    
    def main():
        app = QApplication(sys.argv)
    
        qml_engine = QQmlEngine()
    
        component = QQmlComponent(qml_engine)
        component.setData(textwrap.dedent("""\
            import QtQuick 2.0
    
            Rectangle {
                Component.onCompleted: {
                    console.log("created");
                }
                Component.onDestruction: {
                    console.log("destroyed");
                }
            }
            """), QUrl())
    
        item = component.create()
        assert item.parent() is None
    
        # According to sip.dump(), item is owned by C++, but should be owned by
        # Python
        #sip.dump(item)
        # <PyQt5.QtCore.QObject object at 0x7f411e1c69d8>
        #     Reference count: 2
        #     Address of wrapped object: 0x22c0fb0
        #     Created by: C/C++
        #     To be destroyed by: C/C++
        #     Parent wrapper: NULL
        #     Next sibling wrapper: NULL
        #     Previous sibling wrapper: NULL
        #     First child wrapper: NULL
    
        # Explicit transfer of the ownership to Python fixes issue with not
        # destroyed QML item.
        #sip.transferback(item)
    
        del item
        # The QML item should be destroyed at this point, but it's not.
    
        input()
    
    if __name__ == "__main__":
        main()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

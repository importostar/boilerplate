---
title: DataTree
date: 2020-05-07
---
Example Python program DataTree.py

## Modules

* import ast
* from PyQt5.QtCore import Qt
* from PyQt5.QtGui import QCursor
* from PyQt5.QtWidgets import QAbstractItemView, QTreeWidget, QTreeWidgetItem
* from PyQt5.QtWidgets import QMenu

## Classes

* class DataTreeItem(QTreeWidgetItem):
* class DataTree(QTreeWidget):

## Methods

* def __init__(self, user_added):
* def __iter__(self):
* def userAdded(self):
* def pyData(self):
* def setPyData(self, data):
* def cast_to_float(cls, data):
* def make_item(cls,
* def fill_item(cls, item, value):
* def collapse_item(cls, item, value):
* def __init__(self, parent, name, data):
* def collapse(self):
* ##def addItem(self):
* def deleteItem(self):
* def dataChanged(self, *args):
* def contextMenuEvent(self, event):

## Code

Example Python PyQt program :

    import ast
    
    from PyQt5.QtCore import Qt
    from PyQt5.QtGui import QCursor
    from PyQt5.QtWidgets import QAbstractItemView, QTreeWidget, QTreeWidgetItem
    from PyQt5.QtWidgets import QMenu
    
    
    class DataTreeItem(QTreeWidgetItem):
    
        def __init__(self, user_added):
            QTreeWidgetItem.__init__(self)
            self.setExpanded(True)
            self.__user_added = user_added
            self.__data = None
            self._type = None
    
        def __iter__(self):
            for i in range(self.childCount()):
                yield self.child(i)
    
        def userAdded(self):
            return self.__user_added
    
        def pyData(self):
            return self.__data
    
        def setPyData(self, data):
            self.__data = data
    
    
    class DataTree(QTreeWidget):
    
        @classmethod
        def cast_to_float(cls, data):
            if isinstance(data, int):
                return float(data)
            elif isinstance(data, list):
                return [float(el) if isinstance(el, int) else el for el in data]
            else:
                return data
    
        @classmethod
        def make_item(cls,
                      data=None, text=None,
                      fill=False, container=False,
                      user_added=False):
            child = DataTreeItem(user_added)
    
            if text is not None:
                child.setText(0, text)
    
            if data is not None:
                # Cast all integers to floating points to simplify type-checking.
                child.setPyData(cls.cast_to_float(data))
                child.setText(0, str(data) if text is None else text)
    
            if not container:
                child.setFlags(child.flags() | Qt.ItemIsEditable)
            elif data is not None:
                child._type = type(data)
            else:
                child._type = list
    
            if fill and data:
                cls.fill_item(child, data)
    
            return child
    
        @classmethod
        def fill_item(cls, item, value):
            if isinstance(value, dict):
                for key, val in value.items():
                    # Remove the `container` flag to enable the editing of keys.
                    child = cls.make_item(data=val, text=str(key), fill=True,
                                          container=True)
                    # Remove this if parent items should retain data.
                    child.setPyData(None)
                    item.addChild(child)
                return
            elif isinstance(value, list):
                # Determine if this is a bottom-level data element.
                isSuperContainer = any(isinstance(e, (list, dict)) for e in value)
                if isSuperContainer:
                    # Make an empty container item if we aren't at bottom-level.
                    child = cls.make_item(text='[', container=True)
                else:
                    # Comment out `container` flag and `_type` reset to
                    # change display format. See next comment.
                    child = cls.make_item(text=str(value), container=True)
                    child.setPyData(value)
                    child._type = None
    
                for idx, val in enumerate(value):
                    if isinstance(val, (list, dict)):
                        cls.fill_item(child, val)
                    # Uncomment this clause if basic elements should be displayed
                    # as their own items. (i.e. Pos->[X,Y,Z] instead of Pos->X,Y,Z) 
    ##                elif not isSuperContainer:
    ##                    pass
                    else:
                        child.addChild(cls.make_item(val))
            # This clause handles direct (key, val) pairs. (i.e. Age->12)
            else:
                child = cls.make_item(value)
    
            item.addChild(child)
    
        @classmethod
        def collapse_item(cls, item, value):
            for child in item:
                key = child.text(0)
    
                if child._type in (list, dict):
                    val = cls.collapse_item(child, child._type())
                    if isinstance(val, list) and key != '[':
                        val = val[0]
                else:
                    if child.pyData():
                        val = child.pyData()
                    else:
                        val = child.child(0).pyData()
    
                if isinstance(value, list):
                    value.append(val)
                else:
                    value[key] = val
    
            return value
    
        def __init__(self, parent, name, data):
            QTreeWidget.__init__(self, parent)
            self.setSelectionMode(QAbstractItemView.SingleSelection)
            self.setHeaderLabels([name])
    
            root = self.invisibleRootItem()
            root.__class__ = DataTreeItem
            root.setPyData(None)
            root._type = dict
            self.fill_item(root, data)
    
        def collapse(self):
            return self.collapse_item(self.invisibleRootItem(), {})
    
        # See `contextMenuEvent`.
    ##    def addItem(self):
    ##        parent = self.currentItem()
    ##        if not parent:
    ##            parent = self.invisibleRootItem()
    ##
    ##        if parent.pyData() is None or parent.userAdded():
    ##            newItem = self.make_item(text='None', user_added=True)
    ##            parent.addChild(newItem)
    
        def deleteItem(self):
            item = self.currentItem()
            if not item:
                return
    
            parent = item.parent()
            if not parent:
                parent = self.invisibleRootItem()
    
            if parent.pyData() is None:
                parent.removeChild(item)
    
        def dataChanged(self, *args):
            item = self.currentItem()
            oldData = item.pyData()
            newText = item.text(0)
    
            try:
                try:
                    # Try to make something out of the user entry.
                    _data = ast.literal_eval(newText)
                    if isinstance(_data, (tuple, set)):
                        _data = list(_data)
                    newText = str(_data)
                except (ValueError, SyntaxError):
                    # Not a valid entry; try it as a string.
                    _data = newText
                except Exception as e:
                    # Unable to parse entry.
                    raise ValueError(e)
    
                # Numbers are automatically cast to floating points
                # (see `make_item`), but we still display the ints.
                newData = self.cast_to_float(_data)
    
                if oldData is None or item.userAdded():
                    pass
                # Remove this clause to disable type-checking of user entries.
                elif not isinstance(newData, type(oldData)) or (
                    # extra list checking
                    isinstance(newData, list)
                    # check length of list
                    and (len(newData) == len(oldData)
                         # check types of list elements
                         and all(type(a) == type(b)
                                 for a, b in zip(oldData, newData)))):
                    
                    raise TypeError()
            except (TypeError, ValueError):
                # Bad entry. Revert the item's text.
                newText = str(oldData)
                return
            else:
                # Update the item's storage value.
                item.setPyData(newData)
            finally:
                # Update the item's text value.
                item.setText(0, newText)
    
            # Comment out this block to display Pos->[X,Y,Z] instead of Pos->X,Y,Z
            # See the comments in `fill_item` regarding this.
            parent = item.parent()
            if parent:
                parentData = parent.pyData()
                if isinstance(parentData, list):
                    idx = parent.indexOfChild(item)
                    parentData[idx] = newData
                    # Part of the handling to display integers.
                    parent.setText(0, str([_data if i == idx else val \
                                           for i, val in enumerate(parentData)]))
    
        def contextMenuEvent(self, event):
            menu = QMenu(self)
            # Adding items doesn't work quite right. There's a lot of side cases.
    ##        menu.addAction("Add item", lambda: self.addItem())
            menu.addAction("Delete item", self.deleteItem)
            menu.popup(QCursor.pos())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

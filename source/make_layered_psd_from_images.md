---
title: make_layered_psd_from_images
date: 2020-05-07
---
Example Python program make_layered_psd_from_images.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import glob
* import os
* import krita
* from PyQt5 import QtWidgets

## Methods

* def open_document(filepath, show=True):
* def get_layers(doc):
* def make_layered_psd_from_images():

## Code

Example Python PyQt program :

    import glob
    import os
    
    import krita
    from PyQt5 import QtWidgets
    
    
    IMAGES_FILEPATH = QtWidgets.QFileDialog.getExistingDirectory()
    FILEPATHS = sorted(glob.glob(IMAGES_FILEPATH + '/*'))
    print(FILEPATHS)
    
    
    def open_document(filepath, show=True):
        """Open the given filepath as new document
    
        Arguments:
            filepath (str): the filepath of the image to open
            show (bool): should the image get shown in the Krita UI?
        """
        
        k = krita.Krita.instance()
        print('Debug: opening %s' % filepath)
        doc = k.openDocument(filepath)
        if show:
            Application.activeWindow().addView(doc)
        return doc
    
    
    def get_layers(doc):
        """Return layers for given document"""
        nodes = []
        root = doc.rootNode()
        for node in root.childNodes():
            print('Debug: found node of type %s: %s' % (node.type(), node.name()))
            if node.type() == "paintlayer":
                nodes.append(node)
        return nodes
    
    
    
    def make_layered_psd_from_images():
        """Takes a folderpath, scans it for images and produces a layered image"""
    
        
        doc = open_document(FILEPATHS[0], show=False)
        doc_root = doc.rootNode()
        
        docs = []
        docs.append(doc)
    
        all_layers = get_layers(doc)
        for i in range(1, len(FILEPATHS)):
            docx = open_document(FILEPATHS[i], show=False)
            docs.append(docx)
            docx_layers = get_layers(docx)
            for layer in docx_layers:
                all_layers.append(layer.clone())
                # doc.rootNode().addChildNode(layer, parent_node)
        doc_root.setChildNodes(all_layers)
    
        print('Debug: all nodes: %s' % doc.rootNode().childNodes())
        # doc.refreshProjection()
    
        save_filepath = filepath = QtWidgets.QFileDialog.getSaveFileName()[0]
        r = doc.saveAs(save_filepath)
        print('Debug: saved: %s' % save_filepath)
        
        for doc in docs:
            print('Debug: closing %s' % doc)
            doc.close()
    
        print('Debug: Script done')
    
    
    make_layered_psd_from_images()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: create_document
date: 2020-05-07
---
Example Python program create_document.py

## Modules

* import krita

## Methods

* def add_document_to_window():

## Code

Python example

    import krita
    
    def add_document_to_window():
        """Add new document to Krita
    
        Arguments:
            width (int): width in pixels
            height (int): height in pixels
            name (str): name of the image (not the filename of the document)
            colorModel (str): color model of document, e.g. "RGBA", "XYZA", "LABA", "CMYKA", "GRAYA", "YCbCrA"
            colorDepth (str): color depth, e.g. "U8", "U16", "F16" or "F32"
            profile (str): The name of an icc profile that is known to Krita
            resolution (float): the resolution in points per inch
            
        Returns:
            the created document
        
        """
        k = krita.Krita.instance()
        doc = k.createDocument(100, 100, "Test", "RGBA", "U8", "", 120.0)
        Application.activeWindow().addView(doc)
        return doc
        
    doc = add_document_to_window()
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

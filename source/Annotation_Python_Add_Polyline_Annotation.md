---
title: Annotation_Python_Add_Polyline_Annotation
date: 2020-05-07
---
Example Python program Annotation_Python_Add_Polyline_Annotation.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from groupdocs_annotation_cloud import *
* import groupdocs_annotation_cloud
* from Common_Utilities.Utils import Common_Utilities

## Classes

* class Annotation_Python_Add_Polyline_Annotation:

## Methods

* def Run(self):

## Code

Python example

    # Import modules
    from groupdocs_annotation_cloud import *
    import groupdocs_annotation_cloud
    
    from Common_Utilities.Utils import Common_Utilities
    
    
    class Annotation_Python_Add_Polyline_Annotation:
        
        @classmethod
        def Run(self):
            # Create instance of the API
            api = Common_Utilities.Get_AnnotateApi_Instance()
            
            try:        
                a1 = groupdocs_annotation_cloud.AnnotationInfo()
                a1.annotation_position = groupdocs_annotation_cloud.Point()
                a1.annotation_position.x = 852
                a1.annotation_position.y = 59.388262910798119
                a1.box = groupdocs_annotation_cloud.Rectangle()
                a1.box.x = 375.89276123046875
                a1.box.y = 59.388263702392578
                a1.box.width = 88.7330551147461
                a1.box.height = 37.7290153503418
                a1.page_number = 2
                a1.pen_color = 1201033
                a1.pen_style = 0
                a1.pen_width = 1
                a1.opacity = 0.7
                a1.type = "Polyline"
                a1.text = "This is polyline annotation"
                a1.creator_name = "Anonym A."
        
                request = PostAnnotationsRequest("annotationdocs\\ten-pages.docx", [a1])
                api.post_annotations(request)
                
                print("Expected response type is void: Polyline Annotation added.")
            except ApiException as e:
                print("Exception when calling AnnotateAPI: {0}".format(e.message))

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

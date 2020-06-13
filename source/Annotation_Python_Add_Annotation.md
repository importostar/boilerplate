---
title: Annotation_Python_Add_Annotation
date: 2020-05-07
---
Example Python program Annotation_Python_Add_Annotation.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from groupdocs_annotation_cloud import *
* import groupdocs_annotation_cloud
* from Common_Utilities.Utils import Common_Utilities

## Classes

* class Annotation_Python_Add_Annotation:

## Methods

* def Run(self):

## Code

Python example

    # Import modules
    from groupdocs_annotation_cloud import *
    import groupdocs_annotation_cloud
    
    from Common_Utilities.Utils import Common_Utilities
    
    
    class Annotation_Python_Add_Annotation:
        
        @classmethod
        def Run(self):
            # Create instance of the API
            api = Common_Utilities.Get_AnnotateApi_Instance()
            
            try:        
                a = AnnotationInfo()
                a.annotation_position = Point()
                a.annotation_position.x = 852
                a.annotation_position.y = 59.388262910798119
                
                a.box = Rectangle()
                a.box.x = 375.89276123046875
                a.box.y = 59.388263702392578
                a.box.width = 88.7330551147461
                a.box.height = 37.7290153503418
                a.page_number = 0
                a.pen_color = 1201033
                a.pen_style = 0
                a.pen_width = 1
                a.type = "Area"
                a.creator_name = "Anonym A."    
                
                request = PostAnnotationsRequest("annotationdocs\\one-page.docx", [a])
                api.post_annotations(request)
                
                print("Expected response type is void: Annotation added.")
            except ApiException as e:
                print("Exception when calling Annotation_Python_Add_Annotation: {0}".format(e.message))

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

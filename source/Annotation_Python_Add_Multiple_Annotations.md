---
title: Annotation_Python_Add_Multiple_Annotations
date: 2020-05-07
---
Example Python program Annotation_Python_Add_Multiple_Annotations.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from groupdocs_annotation_cloud import *
* import groupdocs_annotation_cloud
* from Common_Utilities.Utils import Common_Utilities

## Classes

* class Annotation_Python_Add_Multiple_Annotations:

## Methods

* def Run(self):

## Code

Python example

    # Import modules
    from groupdocs_annotation_cloud import *
    import groupdocs_annotation_cloud
    
    from Common_Utilities.Utils import Common_Utilities
    
    
    class Annotation_Python_Add_Multiple_Annotations:
        
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
                a1.page_number = 0
                a1.pen_color = 1201033
                a1.pen_style = 0
                a1.pen_width = 1
                a1.opacity = 0.7
                a1.type = "Distance"
                a1.text = "This is distance annotation"
                a1.creator_name = "Anonym A."
        
                a2 = groupdocs_annotation_cloud.AnnotationInfo()
                a2.annotation_position = groupdocs_annotation_cloud.Point()
                a2.annotation_position.x = 852
                a2.annotation_position.y = 59.388262910798119
                a2.box = groupdocs_annotation_cloud.Rectangle()
                a2.box.x = 375.89276123046875
                a2.box.y = 59.388263702392578
                a2.box.width = 88.7330551147461
                a2.box.height = 37.7290153503418
                a2.page_number = 2
                a2.pen_color = 1201033
                a2.pen_style = 0
                a2.pen_width = 1
                a2.opacity = 0.7
                a2.type = "Area"
                a2.text = "This is area annotation"
                a2.creator_name = "Anonym A."
        
                a3 = groupdocs_annotation_cloud.AnnotationInfo()
                a3.annotation_position = groupdocs_annotation_cloud.Point()
                a3.annotation_position.x = 852
                a3.annotation_position.y = 59.388262910798119
                a3.box = groupdocs_annotation_cloud.Rectangle()
                a3.box.x = 375.89276123046875
                a3.box.y = 59.388263702392578
                a3.box.width = 88.7330551147461
                a3.box.height = 37.7290153503418
                a3.page_number = 4
                a3.opacity = 0.7
                a3.type = "Point"
                a3.text = "This is point annotation"
                a3.creator_name = "Anonym A."
        
                a4 = groupdocs_annotation_cloud.AnnotationInfo()
                a4.annotation_position = groupdocs_annotation_cloud.Point()
                a4.annotation_position.x = 852
                a4.annotation_position.y = 59.388262910798119
                a4.box = groupdocs_annotation_cloud.Rectangle()
                a4.box.x = 375.89276123046875
                a4.box.y = 59.388263702392578
                a4.box.width = 88.7330551147461
                a4.box.height = 37.7290153503418
                a4.page_number = 5
                a4.pen_color = 1201033
                a4.pen_style = 0
                a4.pen_width = 1
                a4.opacity = 0.7
                a4.type = "Arrow"
                a4.text = "This is arrow annotation"
                a4.creator_name = "Anonym A."
        
                request = PostAnnotationsRequest("annotationdocs\\ten-pages.docx", [a1, a2, a3, a4])
                api.post_annotations(request)
                
                print("Expected response type is void: Multiple Annotations added.")
            except ApiException as e:
                print("Exception when calling AnnotateAPI: {0}".format(e.message))

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: Annotation_Python_Run_Examples
date: 2020-05-07
---
Example Python program Annotation_Python_Run_Examples.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import groupdocs_annotation_cloud
* from Common_Utilities.Utils import Common_Utilities
* from Supported_File_Formats.Annotation_Python_Get_All_Supported_Formats import Annotation_Python_Get_All_Supported_Formats
* # from Working_With_Storage.Annotation_Python_Storage_Exist import Annotation_Python_Storage_Exist
* # from Working_With_Storage.Annotation_Python_Object_Exists import Annotation_Python_Object_Exists
* # from Working_With_Storage.Annotation_Python_Get_File_Versions import Annotation_Python_Get_File_Versions
* # from Working_With_Storage.Annotation_Python_Get_Disc_Usage import Annotation_Python_Get_Disc_Usage
* # from Working_With_Folder.Annotation_Python_Create_Folder import Annotation_Python_Create_Folder
* # from Working_With_Folder.Annotation_Python_Copy_Folder import Annotation_Python_Copy_Folder
* # from Working_With_Folder.Annotation_Python_Get_Files_List import Annotation_Python_Get_Files_List
* # from Working_With_Folder.Annotation_Python_Move_Folder import Annotation_Python_Move_Folder
* # from Working_With_Folder.Annotation_Python_Delete_Folder import Annotation_Python_Delete_Folder
* # from Working_With_Files.Annotation_Python_Upload_File import Annotation_Python_Upload_File
* # from Working_With_Files.Annotation_Python_Download_File import Annotation_Python_Download_File
* # from Working_With_Files.Annotation_Python_Copy_File import Annotation_Python_Copy_File
* # from Working_With_Files.Annotation_Python_Move_File import Annotation_Python_Move_File
* # from Working_With_Files.Annotation_Python_Delete_File import Annotation_Python_Delete_File
* # from Document_Information.Annotation_Python_DocumentInfo_File import Annotation_Python_DocumentInfo_File
* # from Working_With_Annotations.Annotation_Python_Add_Multiple_Annotations import Annotation_Python_Add_Multiple_Annotations
* # from Working_With_Annotations.Annotation_Python_Add_Area_Annotation import Annotation_Python_Add_Area_Annotation
* # from Working_With_Annotations.Annotation_Python_Add_Arrow_Annotation import Annotation_Python_Add_Arrow_Annotation
* # from Working_With_Annotations.Annotation_Python_Add_Point_Annotation import Annotation_Python_Add_Point_Annotation
* # from Working_With_Annotations.Annotation_Python_Add_Polyline_Annotation import Annotation_Python_Add_Polyline_Annotation
* # from Working_With_Annotations.Annotation_Python_Add_Text_Annotation import Annotation_Python_Add_Text_Annotation
* # from Working_With_Annotations.Annotation_Python_Add_TextField_Annotation import Annotation_Python_Add_TextField_Annotation
* # from Working_With_Annotations.Annotation_Python_Add_TextRedaction_Annotation import Annotation_Python_Add_TextRedaction_Annotation
* # from Working_With_Annotations.Annotation_Python_Add_TextReplacement_Annotation import Annotation_Python_Add_TextReplacement_Annotation
* # from Working_With_Annotations.Annotation_Python_Add_TextStrikeout_Annotation import Annotation_Python_Add_TextStrikeout_Annotation
* # from Working_With_Annotations.Annotation_Python_Add_TextUnderline_Annotation import Annotation_Python_Add_TextUnderline_Annotation
* # from Working_With_Annotations.Annotation_Python_Add_Watermark_Annotation import Annotation_Python_Add_Watermark_Annotation
* # from Working_With_Annotations.Annotation_Python_Get_Annotation import Annotation_Python_Get_Annotation
* # from Working_With_Annotations.Annotation_Python_Get_Export_Document import Annotation_Python_Get_Export_Document
* # from Working_With_Annotations.Annotation_Python_Get_PDF import Annotation_Python_Get_PDF
* # from Working_With_Annotations.Annotation_Python_Delete_Annotation import Annotation_Python_Delete_Annotation
* # from Working_With_Pages.Annotation_Python_Get_Pages import Annotation_Python_Get_Pages
* # from Working_With_Pages.Annotation_Python_Delete_Pages import Annotation_Python_Delete_Pages

## Code

Python example

    # Import modules
    import groupdocs_annotation_cloud
    
    from Common_Utilities.Utils import Common_Utilities
    from Supported_File_Formats.Annotation_Python_Get_All_Supported_Formats import Annotation_Python_Get_All_Supported_Formats
    
    
    # Get your app_sid and app_key at https://dashboard.groupdocs.cloud (free registration is required).
    Common_Utilities.host_url = "https://api.groupdocs.cloud"  # Put your Host URL here
    Common_Utilities.app_sid = "XXXXX-XXXXX-XXXXX-XXXXX-XXXXX"
    Common_Utilities.app_key = "XXXXXXXXXXXXXXX"
    Common_Utilities.myStorage = "XXXXX"
    
    # #########################################
    # print("Executing Upload Test Files...")
    # Common_Utilities.Upload_Test_Files()
    # #########################################
    
    ###########################################
    #******* Execute Examples *******
    print("*** Executing examples...")
    #******* Execute Examples *******
    ###########################################
    
    #########################################
    print("*** Executing Get_Supported_Formats...")
    #########################################
    
    print("* Executing Annotation_Python_Get_All_Supported_Formats...")
    Annotation_Python_Get_All_Supported_Formats.Run()
    
     
    # ##########################################
    # print("*** Executing Working_With_Storage...")
    # ##########################################
     
    # print("* Executing Annotation_Python_Storage_Exist...")
    # from Working_With_Storage.Annotation_Python_Storage_Exist import Annotation_Python_Storage_Exist
    # Annotation_Python_Storage_Exist.Run()
     
    # print("* Executing Annotation_Python_Object_Exists...")
    # from Working_With_Storage.Annotation_Python_Object_Exists import Annotation_Python_Object_Exists
    # Annotation_Python_Object_Exists.Run()
     
    # print("* Executing Annotation_Python_Get_File_Versions...")
    # from Working_With_Storage.Annotation_Python_Get_File_Versions import Annotation_Python_Get_File_Versions
    # Annotation_Python_Get_File_Versions.Run()
     
    # print("* Executing Annotation_Python_Get_Disc_Usage...")
    # from Working_With_Storage.Annotation_Python_Get_Disc_Usage import Annotation_Python_Get_Disc_Usage
    # Annotation_Python_Get_Disc_Usage.Run()
     
     
    # ##########################################
    # print("*** Executing Working_With_Folder...")
    # ##########################################
     
    # print("* Executing Annotation_Python_Create_Folder...")
    # from Working_With_Folder.Annotation_Python_Create_Folder import Annotation_Python_Create_Folder
    # Annotation_Python_Create_Folder.Run()
     
    # print("* Executing Annotation_Python_Copy_Folder...")
    # from Working_With_Folder.Annotation_Python_Copy_Folder import Annotation_Python_Copy_Folder
    # Annotation_Python_Copy_Folder.Run()
     
    # print("* Executing Annotation_Python_Get_Files_List...")
    # from Working_With_Folder.Annotation_Python_Get_Files_List import Annotation_Python_Get_Files_List
    # Annotation_Python_Get_Files_List.Run()
     
    # print("* Executing Annotation_Python_Move_Folder...")
    # from Working_With_Folder.Annotation_Python_Move_Folder import Annotation_Python_Move_Folder
    # Annotation_Python_Move_Folder.Run()
     
    # print("* Executing Annotation_Python_Delete_Folder...")
    # from Working_With_Folder.Annotation_Python_Delete_Folder import Annotation_Python_Delete_Folder
    # Annotation_Python_Delete_Folder.Run()
     
     
    # ##########################################
    # print("*** Executing Working_With_Files...")
    # ##########################################
     
    # print("* Executing Annotation_Python_Upload_File...")
    # from Working_With_Files.Annotation_Python_Upload_File import Annotation_Python_Upload_File
    # Annotation_Python_Upload_File.Run()
     
    # print("* Executing Annotation_Python_Download_File...")
    # from Working_With_Files.Annotation_Python_Download_File import Annotation_Python_Download_File
    # Annotation_Python_Download_File.Run()
     
    # print("* Executing Annotation_Python_Copy_File...")
    # from Working_With_Files.Annotation_Python_Copy_File import Annotation_Python_Copy_File
    # Annotation_Python_Copy_File.Run()
     
    # print("* Executing Annotation_Python_Move_File...")
    # from Working_With_Files.Annotation_Python_Move_File import Annotation_Python_Move_File
    # Annotation_Python_Move_File.Run()
     
    # print("* Executing Annotation_Python_Delete_File...")
    # from Working_With_Files.Annotation_Python_Delete_File import Annotation_Python_Delete_File
    # Annotation_Python_Delete_File.Run()
    
    
    # ############################################################
    # print("*** Executing Working_With_Document_Information...")
    # ############################################################
    
    # print("* Executing Annotation_Python_DocumentInfo_File...")
    # from Document_Information.Annotation_Python_DocumentInfo_File import Annotation_Python_DocumentInfo_File
    # Annotation_Python_DocumentInfo_File.Run()
    
    
    # ############################################################
    # print("*** Executing Working_With_Annotations...")
    # ############################################################
    
    # print("* Executing Annotation_Python_Add_Multiple_Annotations...")
    # from Working_With_Annotations.Annotation_Python_Add_Multiple_Annotations import Annotation_Python_Add_Multiple_Annotations
    # Annotation_Python_Add_Multiple_Annotations.Run()
    
    # print("* Executing Annotation_Python_Add_Area_Annotation...")
    # from Working_With_Annotations.Annotation_Python_Add_Area_Annotation import Annotation_Python_Add_Area_Annotation
    # Annotation_Python_Add_Area_Annotation.Run()
    
    # print("* Executing Annotation_Python_Add_Arrow_Annotation...")
    # from Working_With_Annotations.Annotation_Python_Add_Arrow_Annotation import Annotation_Python_Add_Arrow_Annotation
    # Annotation_Python_Add_Arrow_Annotation.Run()
    
    # print("* Executing Annotation_Python_Add_Point_Annotation...")
    # from Working_With_Annotations.Annotation_Python_Add_Point_Annotation import Annotation_Python_Add_Point_Annotation
    # Annotation_Python_Add_Point_Annotation.Run()
    
    # print("* Executing Annotation_Python_Add_Polyline_Annotation...")
    # from Working_With_Annotations.Annotation_Python_Add_Polyline_Annotation import Annotation_Python_Add_Polyline_Annotation
    # Annotation_Python_Add_Polyline_Annotation.Run()
    
    # print("* Executing Annotation_Python_Add_Text_Annotation...")
    # from Working_With_Annotations.Annotation_Python_Add_Text_Annotation import Annotation_Python_Add_Text_Annotation
    # Annotation_Python_Add_Text_Annotation.Run()
    
    # print("* Executing Annotation_Python_Add_TextField_Annotation...")
    # from Working_With_Annotations.Annotation_Python_Add_TextField_Annotation import Annotation_Python_Add_TextField_Annotation
    # Annotation_Python_Add_TextField_Annotation.Run()
    
    # print("* Executing Annotation_Python_Add_TextRedaction_Annotation...")
    # from Working_With_Annotations.Annotation_Python_Add_TextRedaction_Annotation import Annotation_Python_Add_TextRedaction_Annotation
    # Annotation_Python_Add_TextRedaction_Annotation.Run()
    
    # print("* Executing Annotation_Python_Add_TextReplacement_Annotation...")
    # from Working_With_Annotations.Annotation_Python_Add_TextReplacement_Annotation import Annotation_Python_Add_TextReplacement_Annotation
    # Annotation_Python_Add_TextReplacement_Annotation.Run()
    
    # print("* Executing Annotation_Python_Add_TextStrikeout_Annotation...")
    # from Working_With_Annotations.Annotation_Python_Add_TextStrikeout_Annotation import Annotation_Python_Add_TextStrikeout_Annotation
    # Annotation_Python_Add_TextStrikeout_Annotation.Run()
    
    # print("* Executing Annotation_Python_Add_TextUnderline_Annotation...")
    # from Working_With_Annotations.Annotation_Python_Add_TextUnderline_Annotation import Annotation_Python_Add_TextUnderline_Annotation
    # Annotation_Python_Add_TextUnderline_Annotation.Run()
    
    # print("* Executing Annotation_Python_Add_Watermark_Annotation...")
    # from Working_With_Annotations.Annotation_Python_Add_Watermark_Annotation import Annotation_Python_Add_Watermark_Annotation
    # Annotation_Python_Add_Watermark_Annotation.Run()
    
    # print("* Executing Annotation_Python_Get_Annotation...")
    # from Working_With_Annotations.Annotation_Python_Get_Annotation import Annotation_Python_Get_Annotation
    # Annotation_Python_Get_Annotation.Run()
    
    # print("* Executing Annotation_Python_Get_Export_Document...")
    # from Working_With_Annotations.Annotation_Python_Get_Export_Document import Annotation_Python_Get_Export_Document
    # Annotation_Python_Get_Export_Document.Run()
    
    # print("* Executing Annotation_Python_Get_PDF...")
    # from Working_With_Annotations.Annotation_Python_Get_PDF import Annotation_Python_Get_PDF
    # Annotation_Python_Get_PDF.Run()
    
    # print("* Executing Annotation_Python_Delete_Annotation...")
    # from Working_With_Annotations.Annotation_Python_Delete_Annotation import Annotation_Python_Delete_Annotation
    # Annotation_Python_Delete_Annotation.Run()
    
    
    # ############################################################
    # print("*** Executing Working_With_Pages...")
    # ############################################################
    
    # print("* Executing Annotation_Python_Get_Pages...")
    # from Working_With_Pages.Annotation_Python_Get_Pages import Annotation_Python_Get_Pages
    # Annotation_Python_Get_Pages.Run()
    
    # print("* Executing Annotation_Python_Delete_Pages...")
    # from Working_With_Pages.Annotation_Python_Delete_Pages import Annotation_Python_Delete_Pages
    # Annotation_Python_Delete_Pages.Run()
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

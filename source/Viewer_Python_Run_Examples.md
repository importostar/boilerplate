---
title: Viewer_Python_Run_Examples
date: 2020-05-07
---
Example Python program Viewer_Python_Run_Examples.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import groupdocs_viewer_cloud
* from Common_Utilities.Utils import Common_Utilities
* from Supported_File_Formats.Viewer_Python_Get_All_Supported_Formats import Viewer_Python_Get_All_Supported_Formats
* # from Working_With_Storage.Viewer_Python_Storage_Exist import Viewer_Python_Storage_Exist
* # from Working_With_Storage.Viewer_Python_Object_Exists import Viewer_Python_Object_Exists
* # from Working_With_Storage.Viewer_Python_Get_File_Versions import Viewer_Python_Get_File_Versions
* # from Working_With_Storage.Viewer_Python_Get_Disc_Usage import Viewer_Python_Get_Disc_Usage
* # from Working_With_Folder.Viewer_Python_Create_Folder import Viewer_Python_Create_Folder
* # from Working_With_Folder.Viewer_Python_Copy_Folder import Viewer_Python_Copy_Folder
* # from Working_With_Folder.Viewer_Python_Get_Files_List import Viewer_Python_Get_Files_List
* # from Working_With_Folder.Viewer_Python_Move_Folder import Viewer_Python_Move_Folder
* # from Working_With_Folder.Viewer_Python_Delete_Folder import Viewer_Python_Delete_Folder
* # from Working_With_Files.Viewer_Python_Upload_File import Viewer_Python_Upload_File
* # from Working_With_Files.Viewer_Python_Download_File import Viewer_Python_Download_File
* # from Working_With_Files.Viewer_Python_Copy_File import Viewer_Python_Copy_File
* # from Working_With_Files.Viewer_Python_Move_File import Viewer_Python_Move_File
* # from Working_With_Files.Viewer_Python_Delete_File import Viewer_Python_Delete_File
* # from Working_With_Document_Information.Viewer_Python_Get_Info_With_Minimal_ViewOptions import Viewer_Python_Get_Info_With_Minimal_ViewOptions
* # from Working_With_Document_Information.Viewer_Python_Get_Info_With_CAD_Options import Viewer_Python_Get_Info_With_CAD_Options
* # from Working_With_Document_Information.Viewer_Python_Get_Info_With_HTML_View_Format import Viewer_Python_Get_Info_With_HTML_View_Format
* # from Working_With_Document_Information.Viewer_Python_Get_Info_With_Image_View_Format import Viewer_Python_Get_Info_With_Image_View_Format 
* # from Working_With_Document_Information.Viewer_Python_Get_Info_With_Image_View_Options_Options import Viewer_Python_Get_Info_With_Image_View_Options_Options
* # from Working_With_Document_Information.Viewer_Python_Get_Info_With_Project_Options import Viewer_Python_Get_Info_With_Project_Options 
* # from Working_With_Document_Information.Viewer_Python_Get_Info_With_Render_Hidden_Pages import Viewer_Python_Get_Info_With_Render_Hidden_Pages
* # from Working_With_Document_Information.Viewer_Python_Get_Info_With_Spreadsheet_Render_Hidden_Rows_Option import Viewer_Python_Get_Info_With_Spreadsheet_Render_Hidden_Rows_Option
* # from Working_With_Document_Information.Viewer_Python_Get_Info_With_SpreadsheetOptions import Viewer_Python_Get_Info_With_SpreadsheetOptions
* # from Working_With_View.Viewer_Python_Create_View_With_Minimal_ViewOptions import Viewer_Python_Create_View_With_Minimal_ViewOptions
* # from Working_With_View.Viewer_Python_Create_View_With_CAD_Options import Viewer_Python_Create_View_With_CAD_Options
* # from Working_With_View.Viewer_Python_Create_View_With_Fonts_Path_Options import Viewer_Python_Create_View_With_Fonts_Path_Options
* # from Working_With_View.Viewer_Python_Create_View_With_HTML_View_Format import Viewer_Python_Create_View_With_HTML_View_Format
* # from Working_With_View.Viewer_Python_Create_View_With_HTML_ViewOptions import Viewer_Python_Create_View_With_HTML_ViewOptions
* # from Working_With_View.Viewer_Python_Create_View_With_Image_View_Format import Viewer_Python_Create_View_With_Image_View_Format
* # from Working_With_View.Viewer_Python_Create_View_With_Project_Options import Viewer_Python_Create_View_With_Project_Options
* # from Working_With_View.Viewer_Python_Create_View_With_Render_Hidden_Pages import Viewer_Python_Create_View_With_Render_Hidden_Pages
* # from Working_With_View.Viewer_Python_Create_View_With_SpreadsheetOptions import Viewer_Python_Create_View_With_SpreadsheetOptions
* # from Working_With_View.Viewer_Python_Create_View_With_Spreadsheet_Render_Hidden_Rows_Option import Viewer_Python_Create_View_With_Spreadsheet_Render_Hidden_Rows_Option
* # from Working_With_View.Viewer_Python_Create_View_With_StartPage_And_CountPages import Viewer_Python_Create_View_With_StartPage_And_CountPages
* # from Working_With_View.Viewer_Python_Delete_View_With_Default_ViewFormat import Viewer_Python_Delete_View_With_Default_ViewFormat
* from Working_With_View.Viewer_Python_Create_View_With_Responsive_HTML import Viewer_Python_Create_View_With_Responsive_HTML
* from Working_With_View.Viewer_Python_Create_View_With_OutputPath import Viewer_Python_Create_View_With_OutputPath

## Code

Python example

    # Import modules
    import groupdocs_viewer_cloud
    from Common_Utilities.Utils import Common_Utilities
    
    # Get your app_sid and app_key at https://dashboard.groupdocs.cloud (free registration is required).
    Common_Utilities.host_url = "https://api.groupdocs.cloud"  # Put your Host URL here
    Common_Utilities.app_sid = "XXXXX-XXXXX-XXXXX"
    Common_Utilities.app_key = "XXXXXXXXXX"
    Common_Utilities.myStorage = "XXXXX"
    
    #########################################
    print("Executing Upload Test Files...")
    Common_Utilities.Upload_Test_Files()
    #########################################
    
    ###########################################
    #******* Execute Examples *******
    print("*** Executing examples...")
    #******* Execute Examples *******
    ###########################################
    
    #########################################
    print("*** Executing Get_Supported_File_Formats...")
    #########################################
    
    print("* Executing Viewer_Python_Get_All_Supported_Formats...")
    from Supported_File_Formats.Viewer_Python_Get_All_Supported_Formats import Viewer_Python_Get_All_Supported_Formats
    Viewer_Python_Get_All_Supported_Formats.Run()
    
    # ##########################################
    # print("*** Executing Working_With_Storage...")
    # ##########################################
    
    # print("* Executing Viewer_Python_Storage_Exist...")
    # from Working_With_Storage.Viewer_Python_Storage_Exist import Viewer_Python_Storage_Exist
    # Viewer_Python_Storage_Exist.Run()
    
    # print("* Executing Viewer_Python_Object_Exists...")
    # from Working_With_Storage.Viewer_Python_Object_Exists import Viewer_Python_Object_Exists
    # Viewer_Python_Object_Exists.Run()
    
    # print("* Executing Viewer_Python_Get_File_Versions...")
    # from Working_With_Storage.Viewer_Python_Get_File_Versions import Viewer_Python_Get_File_Versions
    # Viewer_Python_Get_File_Versions.Run()
    
    # print("* Executing Viewer_Python_Get_Disc_Usage...")
    # from Working_With_Storage.Viewer_Python_Get_Disc_Usage import Viewer_Python_Get_Disc_Usage
    # Viewer_Python_Get_Disc_Usage.Run()
    
    # ##########################################
    # print("*** Executing Working_With_Folder...")
    # ##########################################
    
    # print("* Executing Viewer_Python_Create_Folder...")
    # from Working_With_Folder.Viewer_Python_Create_Folder import Viewer_Python_Create_Folder
    # Viewer_Python_Create_Folder.Run()
    
    # print("* Executing Viewer_Python_Copy_Folder...")
    # from Working_With_Folder.Viewer_Python_Copy_Folder import Viewer_Python_Copy_Folder
    # Viewer_Python_Copy_Folder.Run()
    
    # print("* Executing Viewer_Python_Get_Files_List...")
    # from Working_With_Folder.Viewer_Python_Get_Files_List import Viewer_Python_Get_Files_List
    # Viewer_Python_Get_Files_List.Run()
    
    # print("* Executing Viewer_Python_Move_Folder...")
    # from Working_With_Folder.Viewer_Python_Move_Folder import Viewer_Python_Move_Folder
    # Viewer_Python_Move_Folder.Run()
    
    # print("* Executing Viewer_Python_Delete_Folder...")
    # from Working_With_Folder.Viewer_Python_Delete_Folder import Viewer_Python_Delete_Folder
    # Viewer_Python_Delete_Folder.Run()
    
    # ##########################################
    # print("*** Executing Working_With_Files...")
    # ##########################################
    
    # print("* Executing Viewer_Python_Upload_File...")
    # from Working_With_Files.Viewer_Python_Upload_File import Viewer_Python_Upload_File
    # Viewer_Python_Upload_File.Run()
    
    # print("* Executing Viewer_Python_Download_File...")
    # from Working_With_Files.Viewer_Python_Download_File import Viewer_Python_Download_File
    # Viewer_Python_Download_File.Run()
    
    # print("* Executing Viewer_Python_Copy_File...")
    # from Working_With_Files.Viewer_Python_Copy_File import Viewer_Python_Copy_File
    # Viewer_Python_Copy_File.Run()
    
    # print("* Executing Viewer_Python_Move_File...")
    # from Working_With_Files.Viewer_Python_Move_File import Viewer_Python_Move_File
    # Viewer_Python_Move_File.Run()
    
    # print("* Executing Viewer_Python_Delete_File...")
    # from Working_With_Files.Viewer_Python_Delete_File import Viewer_Python_Delete_File
    # Viewer_Python_Delete_File.Run()
    
    ############################################################
    print("*** Executing Working_With_Document_Information...")
    ############################################################
    
    # print("* Executing Viewer_Python_Get_Info_With_Minimal_ViewOptions...")
    # from Working_With_Document_Information.Viewer_Python_Get_Info_With_Minimal_ViewOptions import Viewer_Python_Get_Info_With_Minimal_ViewOptions
    # Viewer_Python_Get_Info_With_Minimal_ViewOptions.Run()
    
    # print("* Executing Viewer_Python_Get_Info_With_CAD_Options...")
    # from Working_With_Document_Information.Viewer_Python_Get_Info_With_CAD_Options import Viewer_Python_Get_Info_With_CAD_Options
    # Viewer_Python_Get_Info_With_CAD_Options.Run()
    
    # print("* Executing Viewer_Python_Get_Info_With_HTML_View_Format...")
    # from Working_With_Document_Information.Viewer_Python_Get_Info_With_HTML_View_Format import Viewer_Python_Get_Info_With_HTML_View_Format
    # Viewer_Python_Get_Info_With_HTML_View_Format.Run()
    
    # print("* Executing Viewer_Python_Get_Info_With_Image_View_Format...")
    # from Working_With_Document_Information.Viewer_Python_Get_Info_With_Image_View_Format import Viewer_Python_Get_Info_With_Image_View_Format 
    # Viewer_Python_Get_Info_With_Image_View_Format.Run("PNG")
    
    # print("* Executing Viewer_Python_Get_Info_With_Image_View_Options_Options...")
    # from Working_With_Document_Information.Viewer_Python_Get_Info_With_Image_View_Options_Options import Viewer_Python_Get_Info_With_Image_View_Options_Options
    # Viewer_Python_Get_Info_With_Image_View_Options_Options.Run()
    
    # print("* Executing Viewer_Python_Get_Info_With_Project_Options...")
    # from Working_With_Document_Information.Viewer_Python_Get_Info_With_Project_Options import Viewer_Python_Get_Info_With_Project_Options 
    # Viewer_Python_Get_Info_With_Project_Options.Run()
    
    # print("* Executing Viewer_Python_Get_Info_With_Render_Hidden_Pages...")
    # from Working_With_Document_Information.Viewer_Python_Get_Info_With_Render_Hidden_Pages import Viewer_Python_Get_Info_With_Render_Hidden_Pages
    # Viewer_Python_Get_Info_With_Render_Hidden_Pages.Run()
    
    # print("* Executing Viewer_Python_Get_Info_With_Spreadsheet_Render_Hidden_Rows_Option...")
    # from Working_With_Document_Information.Viewer_Python_Get_Info_With_Spreadsheet_Render_Hidden_Rows_Option import Viewer_Python_Get_Info_With_Spreadsheet_Render_Hidden_Rows_Option
    # Viewer_Python_Get_Info_With_Spreadsheet_Render_Hidden_Rows_Option.Run()
    
    # print("* Executing Viewer_Python_Get_Info_With_SpreadsheetOptions...")
    # from Working_With_Document_Information.Viewer_Python_Get_Info_With_SpreadsheetOptions import Viewer_Python_Get_Info_With_SpreadsheetOptions
    # Viewer_Python_Get_Info_With_SpreadsheetOptions.Run()
    
    # ############################################
    # print("*** Executing Working_With_View..")
    # ############################################
    
    # print("* Executing Viewer_Python_Create_View_With_Minimal_ViewOptions...")
    # from Working_With_View.Viewer_Python_Create_View_With_Minimal_ViewOptions import Viewer_Python_Create_View_With_Minimal_ViewOptions
    # Viewer_Python_Create_View_With_Minimal_ViewOptions.Run()
    
    # print("* Executing Viewer_Python_Create_View_With_CAD_Options...")
    # from Working_With_View.Viewer_Python_Create_View_With_CAD_Options import Viewer_Python_Create_View_With_CAD_Options
    # Viewer_Python_Create_View_With_CAD_Options.Run()
    
    # print("* Executing Viewer_Python_Create_View_With_Fonts_Path_Options...")
    # from Working_With_View.Viewer_Python_Create_View_With_Fonts_Path_Options import Viewer_Python_Create_View_With_Fonts_Path_Options
    # Viewer_Python_Create_View_With_Fonts_Path_Options.Run()
    
    # print("* Executing Viewer_Python_Create_View_With_HTML_View_Format...")
    # from Working_With_View.Viewer_Python_Create_View_With_HTML_View_Format import Viewer_Python_Create_View_With_HTML_View_Format
    # Viewer_Python_Create_View_With_HTML_View_Format.Run()
    
    # print("* Executing Viewer_Python_Create_View_With_HTML_ViewOptions...")
    # from Working_With_View.Viewer_Python_Create_View_With_HTML_ViewOptions import Viewer_Python_Create_View_With_HTML_ViewOptions
    # Viewer_Python_Create_View_With_HTML_ViewOptions.Run()
    
    # print("* Executing Viewer_Python_Create_View_With_Image_View_Format...")
    # from Working_With_View.Viewer_Python_Create_View_With_Image_View_Format import Viewer_Python_Create_View_With_Image_View_Format
    # Viewer_Python_Create_View_With_Image_View_Format.Run("PNG")
    
    # print("* Executing Viewer_Python_Create_View_With_Project_Options...")
    # from Working_With_View.Viewer_Python_Create_View_With_Project_Options import Viewer_Python_Create_View_With_Project_Options
    # Viewer_Python_Create_View_With_Project_Options.Run()
    
    # print("* Executing Viewer_Python_Create_View_With_Render_Hidden_Pages...")
    # from Working_With_View.Viewer_Python_Create_View_With_Render_Hidden_Pages import Viewer_Python_Create_View_With_Render_Hidden_Pages
    # Viewer_Python_Create_View_With_Render_Hidden_Pages.Run()
    
    # print("* Executing Viewer_Python_Create_View_With_SpreadsheetOptions...")
    # from Working_With_View.Viewer_Python_Create_View_With_SpreadsheetOptions import Viewer_Python_Create_View_With_SpreadsheetOptions
    # Viewer_Python_Create_View_With_SpreadsheetOptions.Run()
    
    # print("* Executing Viewer_Python_Create_View_With_Spreadsheet_Render_Hidden_Rows_Option...")
    # from Working_With_View.Viewer_Python_Create_View_With_Spreadsheet_Render_Hidden_Rows_Option import Viewer_Python_Create_View_With_Spreadsheet_Render_Hidden_Rows_Option
    # Viewer_Python_Create_View_With_Spreadsheet_Render_Hidden_Rows_Option.Run()
    
    # print("* Executing Viewer_Python_Create_View_With_StartPage_And_CountPages...")
    # from Working_With_View.Viewer_Python_Create_View_With_StartPage_And_CountPages import Viewer_Python_Create_View_With_StartPage_And_CountPages
    # Viewer_Python_Create_View_With_StartPage_And_CountPages.Run()
    
    # print("* Executing Viewer_Python_Delete_View_With_Default_ViewFormat...")
    # from Working_With_View.Viewer_Python_Delete_View_With_Default_ViewFormat import Viewer_Python_Delete_View_With_Default_ViewFormat
    # Viewer_Python_Delete_View_With_Default_ViewFormat.Run()
    
    print("* Executing Viewer_Python_Create_View_With_Responsive_HTML...")
    from Working_With_View.Viewer_Python_Create_View_With_Responsive_HTML import Viewer_Python_Create_View_With_Responsive_HTML
    Viewer_Python_Create_View_With_Responsive_HTML.Run()
    
    print("* Executing Viewer_Python_Create_View_With_OutputPath...")
    from Working_With_View.Viewer_Python_Create_View_With_OutputPath import Viewer_Python_Create_View_With_OutputPath
    Viewer_Python_Create_View_With_OutputPath.Run()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

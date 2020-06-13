---
title: Annotation_Python_Utils
date: 2020-05-07
---
Example Python program Annotation_Python_Utils.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os
* import groupdocs_annotation_cloud

## Classes

* class Common_Utilities:

## Methods

* def Get_AnnotateApi_Instance(self):
* def Get_InfoApi_Instance(self):
* def Get_PreviewApi_Instance(self):
* def Get_SignApi_Instance(self):
* def Get_StorageApi_Instance(self):
* def Get_FolderApi_Instance(self):
* def Get_FileApi_Instance(self):
* def Upload_Test_Files(self):
* def getListOfFiles(self, dirName):

## Code

Python example

    import os
    
    import groupdocs_annotation_cloud
    
    
    class Common_Utilities:
    
        # Get your app_sid and app_key at https://dashboard.groupdocs.cloud (free registration is required).
        app_sid = None
        app_key = None
        host_url = None
        myStorage = None
        
        @classmethod
        def Get_AnnotateApi_Instance(self):
            # Create instance of the API
            return groupdocs_annotation_cloud.AnnotateApi.from_keys(Common_Utilities.app_sid, Common_Utilities.app_key)
        
        @classmethod
        def Get_InfoApi_Instance(self):
            # Create instance of the API
            return groupdocs_annotation_cloud.InfoApi.from_keys(Common_Utilities.app_sid, Common_Utilities.app_key)
        
        @classmethod
        def Get_PreviewApi_Instance(self):
            # Create instance of the API
            return groupdocs_annotation_cloud.PreviewApi.from_keys(Common_Utilities.app_sid, Common_Utilities.app_key)
        
        @classmethod
        def Get_SignApi_Instance(self):
            # Create instance of the API
            return groupdocs_annotation_cloud.SignApi.from_keys(Common_Utilities.app_sid, Common_Utilities.app_key)
        
        @classmethod
        def Get_StorageApi_Instance(self):
            # Create instance of the API
            return groupdocs_annotation_cloud.StorageApi.from_keys(Common_Utilities.app_sid, Common_Utilities.app_key)
        
        @classmethod
        def Get_FolderApi_Instance(self):
            # Create instance of the API
            return groupdocs_annotation_cloud.FolderApi.from_keys(Common_Utilities.app_sid, Common_Utilities.app_key)
        
        @classmethod
        def Get_FileApi_Instance(self):
            # Create instance of the API
            return groupdocs_annotation_cloud.FileApi.from_keys(Common_Utilities.app_sid, Common_Utilities.app_key)
          
        @classmethod  
        def Upload_Test_Files(self):
            
            dirName = os.path.dirname(os.path.dirname(os.path.abspath(__file__))) + "\\Resources\\annotationdocs\\"
            print("dirName: " + dirName)
            TestFiles = Common_Utilities.getListOfFiles(dirName)
            
            # api initialization
            storageApi = Common_Utilities.Get_StorageApi_Instance()
            fileApi = Common_Utilities.Get_FileApi_Instance()
            
            print("Files Count: " + str(len(TestFiles)))
            
            for item in TestFiles:
                print("File to Upload: "+ dirName + item)
                # skip existing file uploading
                fileExistRequest = groupdocs_annotation_cloud.ObjectExistsRequest(dirName + item)
                fileExistsResponse = storageApi.object_exists(fileExistRequest)
                if not fileExistsResponse.exists:                
                    # file content uploading
                    putCreateRequest = groupdocs_annotation_cloud.UploadFileRequest('annotationdocs\\' + item, dirName + item)
                    fileApi.upload_file(putCreateRequest)
                    print("Uploaded missing file: "+ 'annotationdocs\\' + item)
            
            print("File Uploading completed..")
            
        @classmethod  
        def getListOfFiles(self, dirName):
            # create a list of file and sub directories 
            # names in the given directory 
            listOfFile = os.listdir(dirName)
            allFiles = list()
            # Iterate over all the entries
            for entry in listOfFile:
                # Create full path
                fullPath = os.path.join("", entry)
                # If entry is a directory then get the list of files in this directory 
                if os.path.isdir(fullPath):
                    allFiles = allFiles + Common_Utilities.getListOfFiles(fullPath)
                else:
                    allFiles.append(fullPath)
                        
            return allFiles

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

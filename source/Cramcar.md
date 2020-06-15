---
title: Cramcar
date: 2020-05-07
---
Example Python program Cramcar.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import PyPDF2
* import re
* import tkinter
* from tkinter import *
* import os.path
* from client import *

## Methods

* def create_modes():
* def reveal():
* def create_mode():
* def modifier_mode():
* def reader():
* def text_convert():
* def writeto_disk():
* def edit_save():
* def editor():
* def edit_mode():
* def read_mode():
* def share():
* def share_mode():
* def back_comm():
* def downloader():
* def download_mode():
* def download():

## Code

Python tkinter example

    import PyPDF2
    import re
    import tkinter
    from tkinter import *
    import os.path
    from client import *
    #test sharing pdfs as well as work error correcting codes (failed to connect, not right type of file, etc) , testers for input,also rename and create ico and check file type and filter what is typed and edit how binary looks on the screen and download mode and edit pack_forget for various pages and document also work on multi connections on server . check files to see if real, expand file size, check enteries . get() validity, new pack_forgets in back, and clear inserts after sends or saves, and debinarize files for viewing only, implement IP address connect
    top=tkinter.Tk()
    var = IntVar()
    varchoice=IntVar()
    results_var=''
    mode_type=''
    def create_modes():
       Create_mode.pack_forget()
       Edit_mode.pack_forget()
       Read_mode.pack_forget()
       Share_mode.pack_forget()
       pdf.insert(0,'What PDF would you like to dissect?')
       pdf.pack()
       selection.insert(0,'Select START word to form 1st parameter to select passage')
       selection2.insert(0,'Select END word to form 2nd parameter to select passage')
       selection.pack()
       selection2.pack()
       offset.insert(0,'How many offset spaces do you need?')
       offset.pack()
       R1.pack(anchor = W)
       R2.pack(anchor = W)
       page.insert(0,'Which Page do you want to select to begin?')
       page2.insert(0,'Which Page do you want to select to end?')
       page.pack()
       page2.pack()
       cram.insert(0,"Save CramCard as")
       cram.pack()
       citation.insert(0,"Enter a citation for the work being quoted.")
       citation.pack()
    def reveal():
       text_convert()
       more_mode.pack_forget()
       save.pack()
       back.pack()
    def create_mode():
       create_modes()
       send.pack()
    def modifier_mode():
       output_line.pack_forget()
       cram.pack_forget()
       more_mod.pack_forget()
       save.pack_forget()
       create_modes()
       moddd.pack()
       back.pack()
    def reader():
       directory_name=CRAM_reader.get()
       content=open(directory_name,'rb')
       for contents in content:
          content_b=contents
          retrieve_line.insert(END,content_b)
       retrieve_line.pack()
       content.close() 
       back.pack()
    def text_convert():
       global results_var
       pdfFileObj = open('Docs/'+pdf.get()+'.pdf', 'rb')
       pdfReader = PyPDF2.PdfFileReader(pdfFileObj)
       #pdfReader.numPages
       for x in range(int(page.get()),int(page2.get())):
          if page.get()!='0' and page2.get()!='0':
             pages=int(x-1)
             pageObj = pdfReader.getPage(pages)
             pa=pageObj.extractText()
             res=re.findall(str(selection.get())+"(.*?)"+str(selection2.get()),pa,re.DOTALL)
             print(res)
             for results in res:
                result=results.replace('\n','')
                print(result)
                results_var=results
       output_line.insert(END,results_var)
       output_line.pack()
       more_mod.pack()
       save.pack()
       back.pack()
    def writeto_disk():
             file_check=os.path.isfile('cards/'+'#'+str(cram.get())+'.CRAM')
             if file_check!=True:
                cramcard=open('cards/'+'#'+str(cram.get())+'.CRAM','wb')
                input_line.insert(END,results_var)
                input_line.pack()
                offset_set=var
                if var=="1":
                   cramcard.write(input_line[:-offset_set].encode())
                if var=="2":
                   cramcard.write(input_line[offset_set:].encode())
                else:
                   cramcard.write(results_var.encode())  
             if(os.path.isfile('cards/'+'#'+str(cram.get())+'.CRAM')):
                cramcard=open('cards/'+'#'+str(cram.get())+'.CRAM','a')
                for content in cramcard:
                   input_line.insert(END,content+"\n"+results_var)
                   input_line.pack()
                offset_set=var
                if var=="1":
                   cramcard.write(input_line.get()[:-offset_set].encode())
                   cramcard.close()
                if var=="2":
                   cramcard.write(inputt_line.get()[offset_set:].encode())
                   cramcard.close()
                else:
                   cramcard.write(output_line.get().encode())
                cramcard.close()
             back.pack()
    def edit_save():
       edited_doc=open(CRAM_reader.get(),'wb')
       to_d=eretrieve_line.get("1.0",END)
       for content in to_d:
          edited_doc.write(content.encode())
       edited_doc.close()
       back_comm()
    def editor():
       directory_name=CRAM_reader.get()
       content=open(directory_name,'rb')
       for contents in content:
          eretrieve_line.insert(END,str(contents))
       eretrieve_line.pack()
       content.close()
       back.pack()
       edit_s.pack()
     
    
    def edit_mode():
       Create_mode.pack_forget()
       Edit_mode.pack_forget()
       Read_mode.pack_forget()
       Share_mode.pack_forget()
       CRAM_reader.insert(0,'Please Enter a CramCard to edit')
       CRAM_reader.pack()
       Edit.pack()
       mod.pack()
       back.pack()
    def read_mode():
       Create_mode.pack_forget()
       Edit_mode.pack_forget()
       Read_mode.pack_forget()
       Share_mode.pack_forget()
       CRAM_reader.insert(0,'Enter an existing CramCard to read it')
       CRAM_reader.pack()
       opener.pack()
       back.pack()
    def share():
       if PDF_yes=='yes' or PDF_yes=='Yes' or PDF_yes=='YES':
          conn(shared.get(),shared_name.get(),shared_file.get(),PDF_yes.get(),'OTHER','none')
       else:
          conn(shared.get(),shared_name.get(),shared_file.get(),'no')
       back_comm()
    def share_mode():
       Create_mode.pack()
       Edit_mode.pack()
       Read_mode.pack()
       Share_mode.pack() 
       shared.delete(0, END)
       shared_file.delete(0, END)
       shared_name.delete(0, END)
       PDF_yes.insert(0,"If you want to share a PDF instead say yes. Otherwise leave blank.")
       PDF_yes.pack()
       shared.insert(0,"Please type the server you want to share with")
       shared.pack()
       shared_file.insert(0,"Please enter the file you would like to share")
       shared_file.pack()
       shared_name.insert(0,"What would you like to name the file?")
       shared_name.pack()
       sharer.pack()
       back.pack()
    def back_comm():
       Create_mode.pack()
       Edit_mode.pack()
       Read_mode.pack()
       Share_mode.pack() 
       output_line.pack_forget()
       input_line.pack_forget()
       retrieve_line.pack_forget()
       eretrieve_line.pack_forget()
       CRAM_reader.pack_forget()
       R1.pack_forget()
       R2.pack_forget()
       offset.pack_forget()
       pdf.pack_forget()
       cram.pack_forget()
       selection.pack_forget()
       selection2.pack_forget()
       page2.pack_forget()
       citation.pack_forget()
       page.pack_forget()
       back.pack_forget()
       Edit.pack_forget()
       edit_s.pack_forget()
       shared.pack_forget()
       shared_file.pack_forget()
       sharer.pack_forget()
       shared_name.pack_forget()
    def downloader():
       conn(serverdownload_ip.get(),'no','no','no','get_file',fileto_download.get())
       back_comm()
    def download_mode():
       download_conn=conn(serverdownload_ip.get(),'no','no','no','download','none')
       #put list on screen
       serverdownload_ip.pack_forget()
       download_list.pack_forget()
       fileto_download.insert(0,'Please enter a file to download')
       fileto_download.pack()
       back.pack()
       downloadfrom_server.pack()
    def download():
       Create_mode.pack_forget()
       Edit_mode.pack_forget()
       Read_mode.pack_forget()
       Share_mode.pack_forget()
       serverdownload_ip.pack()
       download_list.pack()
       back.pack()
    Create_mode=tkinter.Button(top,text="WRITE Text", command=create_mode) 
    Edit_mode=tkinter.Button(top,text="EDIT Text", command=edit_mode) 
    Read_mode=tkinter.Button(top,text="READ Text", command=read_mode)
    Share_mode=tkinter.Button(top,text="SHARE Text",command=share_mode)
    R1 = Radiobutton(top, text="Offset Right", variable=var, value=1)
    offset=Entry(top,bd=5,width=35)
    R2 = Radiobutton(top, text="Offset Left", variable=var, value=2)
    pdf=Entry(top,bd=5,width=32)
    cram=Entry(top,bd=5,width=16)
    page2=Entry(top,bd=5,width=32)
    selection=Entry(top,bd=5, width=40)
    selection2=Entry(top,bd=5, width=40)
    input_line=Text(top,bd=5,height=20,width=35)
    output_line=Text(top,bd=5,height=20,width=35)
    retrieve_line=Text(top,bd=5,height=20,width=35)
    eretrieve_line=Text(top,bd=5,height=20,width=35)
    CRAM_reader=Entry(top,bd=5,width=32)
    citation=Entry(top,bd=5, width=40)
    page=Entry(top,bd=5,width=32)
    send=tkinter.Button(top,text="SELECT Text",command=reveal)
    opener=tkinter.Button(top,text="OPEN Text",command=reader)
    back=tkinter.Button(top,text="Back",command=back_comm)
    edit_s=tkinter.Button(top,text="Save",command=edit_save)
    Edit=tkinter.Button(top,text="Edit Text", command=editor) 
    sharer=tkinter.Button(top,text="Share", command=share)
    shared=Entry(top,bd=5,width=32)
    shared_file=Entry(top,bd=5,width=32)
    shared_name=Entry(top,bd=5,width=32)
    save=tkinter.Button(top,text="Save", command=writeto_disk)
    mod=tkinter.Button(top,text="Combine with another PDF", command=modifier_mode)
    moddd=tkinter.Button(top,text="Add", command=text_convert)
    more_mod=tkinter.Button(top,text="Mod", command=modifier_mode)
    PDF_yes=Entry(top,bd=5,width=32)
    download=tkinter.Button(top,text="Download",command=download)
    serverdownload_ip=Entry(top,bd=5,width=32)
    download_list=tkinter.Button(top,text="Get file list.",command=download_mode)
    fileto_download=Entry(top,bd=5,width=32)
    downloadfrom_server=tkinter.Button(top,text="Get file.",command=downloader)
    Create_mode.pack()
    Edit_mode.pack()
    Read_mode.pack()
    Share_mode.pack()
    download.pack()
    top.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

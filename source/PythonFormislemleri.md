---
title: PythonFormislemleri
date: 2020-05-07
---
Example Python program PythonFormislemleri.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from tkinter import *  
* from tkinter import font
* from functools import partial
* import time
* from tkinter import messagebox

## Methods

* def saatbaslat():
* def YeniPencere():
* def on_closing():

## Code

Python tkinter example

    #package tanımlamaları
    from tkinter import *  
    from tkinter import font
    from functools import partial
    import time
    from tkinter import messagebox
    
    #@mmyuksel.com
    
    #Anaform tanımlama
    frmana = Tk()
    frmana.wm_attributes("-topmost", 1)
    ekranEn = frmana.winfo_screenwidth()
    ekranBoy = frmana.winfo_screenmmheight()
    ekranMargin = ekranEn / 4;
    
    #Ana form için temel atamalar
    frmana.title("Ana Form")
    frmana.geometry(str(int(ekranEn / 2)) + "x" + str("600") + "+" + str(int(ekranMargin)) + "+30")
    
    #label tanımlama
    lbad = Label(text="Adınız:", fg="red", bg="#ffffff", relief="raised", bd=7, height=1, width=10, padx=11,
                 state="disabled", font=("Tahoma", 9, "bold"), anchor="w")
    #anchor bilgisi aşağıda açıklanmıştır. 
    lbad.pack()
    #pack() komutu geometrik düzende nesneyi konumlandırır
    #label tanımla işlemi sonu
    
    #bu işlem ile tanımlı font bilgisi yazdırılıyor
    print(font.families())
    
    
    btTamam = Button(text="Tamam")
    btTamam.pack(fill="x")
    # Değer 	Anlamı
    # x 	x düzlemine doğru uzat
    # y 	y düzlemine doğru uzat
    # both 	her iki düzleme doğru uzat
    
     
    #Birimler
    # Değer  Anlamı
    # c 	santimetre
    # i 	inç
    # m 	milimetre
    # p 	point
    
    def saatbaslat():
        lbad["text"] = time.strftime("%H:%M:%S")
        frmana.after(1000, saatbaslat)
    
    #yeni button tanımlamamız 
    btDegistr = Button(text="Degiştir", cursor="hand2")
    btDegistr.pack(expand=1) 
    #tanımlanan butona event tanımla
    btDegistr["command"] = partial(saatbaslat)
    #saat yazısının güncellenmesi için gerekli flash()
    btDegistr.flash()
    
    btTest = Button(text="Test Pasif")
    btTest.pack(anchor="nw")
    # n 	kuzey
    # s 	güney
    # e 	doğu
    # w 	batı
    # ne 	kuzeydoğu
    # nw 	kuzeybatı
    # se 	güneydoğu
    # sw 	güneybatı
    # center orta
    btTest["state"] = "disabled"
    
    #yeni fonksiyon tanımlaması
    def YeniPencere():
       #yeni form tanımlama
        pencere2 = Tk()
        pencere2.wm_attributes("-topmost", 1)
        print("Yeni form oluşturuldu")
    
    btYeni = Button(text="Yeni 1",width=10)
    btYeni["command"] = partial(YeniPencere)
    btYeni.place(x=10, y=80)
    #Pack yerine place komutu ile pozisyon atamsı yapabiliyoruz
    
    #relx=0.5, rely=0.5 verilirse repsonsible oluyor
    
    #delege edilmiş fonksiyonumuz
    def on_closing():
        if messagebox.askokcancel("Uyarı", "Uygulama Kapatılsın mı?"):
            frmana.destroy()
    
    #delegasyon tanımlama
    frmana.protocol("WM_DELETE_WINDOW", on_closing)
    
    #tüm düzenlemelerin ekranda güncellenmesi
    frmana.update()
    mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

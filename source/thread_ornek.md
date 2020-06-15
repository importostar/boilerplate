---
title: thread_ornek
date: 2020-05-07
---
Example Python program thread_ornek.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from threading import Thread
* import time
* from random import randint

## Methods

* def func1(a,b, result, idx):
* def func2(a,b, result, idx):
* def func3(a,b,c, result, idx):

## Code

Python example

    from threading import Thread
    import time
    from random import randint
    
    
    # Uc fonksiyon, uzun calisma icin sleep kullandik.
    # her biri ayri bir thread olarak calisip, en uzun sure calisan bitince sonuclari yazacaktir.
    def func1(a,b, result, idx):
        sleepsec = randint(5,10)
        print("func1, sleeping ", sleepsec)
        time.sleep(sleepsec)
        result[idx] = a+b
        print("func1  finished, value ", a+b)
        
    
    def func2(a,b, result, idx):
        sleepsec = randint(5,10)
        print("func2, sleeping ", sleepsec)
        time.sleep(sleepsec)
        result[idx] = a * b
        print("func2  finished, value ", a*b)
    
    def func3(a,b,c, result, idx):
        sleepsec = randint(5,10)
        print("func3, sleeping ", sleepsec)
        time.sleep(sleepsec)
        result[idx] = a - b + c
        print("func3  finished, value ", a-b+c)
    
    if __name__ == "__main__":
        a = 10
        b = 8
        c = 4
        
        threads = []   # fonksiyonlar thread seklinde bu diziye doldurulacaklar.
        results = [None] *3  # sonuclari buraya dolduracagiz
        threads.append(Thread(target=func1, args=(a,b,results,0,)))
        # sonuclarin doldurulacagi dizi ve hangi indekse cevabi yazacagi parametre olarak veriliyor.
        threads.append(Thread(target=func2, args=(a,b,results,1,)))
        threads.append(Thread(target=func3, args=(a,b,c,results,2,)))                   
    
        #threadleri baslat
        for t in threads:
            t.start()
    
        #hepsinin sonlanmasini beklemesini sagla
        for t in threads:
            t.join()
    
        #bu satira butun threadler bitince gelebilecek, sonuclari yaz
        for r in results:
            print(r)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: imagescrape
date: 2020-05-07
---
Example Python program imagescrape.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from selenium import webdriver
* from selenium.webdriver.support.ui import WebDriverWait
* from selenium.webdriver.support import expected_conditions as ec
* from selenium.webdriver.common.by import By
* from bs4 import BeautifulSoup
* from urllib.request import urlretrieve
* import os
* import tkinter.filedialog as tkFileDialog
* import tkinter as Tkinter
* import tkinter.constants as Tkconstants
* import time

## Methods

* def imagescrape():

## Code

Python tkinter example

    from selenium import webdriver
    from selenium.webdriver.support.ui import WebDriverWait
    from selenium.webdriver.support import expected_conditions as ec
    from selenium.webdriver.common.by import By
    from bs4 import BeautifulSoup
    from urllib.request import urlretrieve
    import os
    import tkinter.filedialog as tkFileDialog
    import tkinter as Tkinter
    import tkinter.constants as Tkconstants
    import time
    
    def imagescrape():
        try:
            driver = webdriver.Chrome()
            driver.maximize_window()
            for i in range(1, searchPage + 1):
                url = "https://www.shutterstock.com/search?searchterm=" + searchTerm + "&sort=popular&image_type=all&search_source=base_landing_page&language=en&page=" + str(i)
                driver.get(url)
                data = driver.execute_script("return document.documentElement.outerHTML")
                print("Page " + str(i))
                scraper = BeautifulSoup(data, "lxml")
                img_container = scraper.find_all("div", {"class":"img-wrap"})
                for j in range(0, len(img_container)-1):
                    img_array = img_container[j].find_all("img")
                    img_src = img_array[0].get("src")
                    name = img_src.rsplit("/", 1)[-1]
                    try:
                        urlretrieve(img_src, os.path.join(scrape_directory, os.path.basename(img_src)))
                        print("Scraped " + name)
                    except Exception as e:
                        print(e)
            driver.close()
        except Exception as e:
            print(e)
    
    print("ShutterScrape v1.1")

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

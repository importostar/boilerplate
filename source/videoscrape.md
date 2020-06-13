---
title: videoscrape
date: 2020-05-07
---
Example Python program videoscrape.py
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

* def videoscrape():

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
    
    def videoscrape():
        try:
            driver = webdriver.Chrome()
            driver.maximize_window()
            for i in range(1, searchPage + 1):
                url = "https://www.shutterstock.com/video/search/" + searchTerm + "?page=" + str(i)
                driver.get(url)
                print("Page " + str(i))
                for j in range (0, 50):
                    while True:
                        container = driver.find_elements_by_xpath("//div[@data-automation='VideoGrid_video_videoClipPreview_" + str(j) + "']")
                        if len(container) != 0:
                            break
                        if len(driver.find_elements_by_xpath("//div[@data-automation='VideoGrid_video_videoClipPreview_" + str(j + 1) + "']")) == 0 and i == searchPage:
                            driver.close()
                            return
                        time.sleep(10)
                        driver.get(url)
                    container[0].click()
                    while True:
                        wait = WebDriverWait(driver, 60).until(ec.visibility_of_element_located((By.XPATH, "//video[@data-automation='VideoPlayer_video_video']")))
                        video_url = driver.current_url
                        data = driver.execute_script("return document.documentElement.outerHTML")
                        scraper = BeautifulSoup(data, "lxml")
                        video_container = scraper.find_all("video", {"data-automation":"VideoPlayer_video_video"})
                        if len(video_container) != 0:
                            break
                        time.sleep(10)
                        driver.get(video_url)
                    video_array = video_container[0].find_all("source")
                    video_src = video_array[1].get("src")
                    name = video_src.rsplit("/", 1)[-1]
                    try:
                        urlretrieve(video_src, os.path.join(scrape_directory, os.path.basename(video_src)))
                        print("Scraped " + name)
                    except Exception as e:
                        print(e)
                    driver.get(url)
        except Exception as e:
            print(e)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

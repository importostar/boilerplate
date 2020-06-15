---
title: set_codes
date: 2020-05-07
---
Example Python program set_codes.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import time
* import os
* import csv
* from selenium import webdriver
* from selenium.webdriver.chrome.service import Service
* from selenium.webdriver.support.ui import WebDriverWait
* from selenium.webdriver.support import expected_conditions as EC
* from selenium.webdriver.chrome.options import Options
* from selenium.webdriver.common.by import By
* from selenium.common.exceptions import TimeoutException
* from tkinter import Tk
* from tkinter.filedialog import askopenfilename

## Methods

* def setCodes(driver, code):

## Code

Python tkinter example

    import time
    import os
    import csv
    
    #### Selenium to run Headless Chrome ####
    from selenium import webdriver
    from selenium.webdriver.chrome.service import Service
    from selenium.webdriver.support.ui import WebDriverWait
    from selenium.webdriver.support import expected_conditions as EC
    from selenium.webdriver.chrome.options import Options
    from selenium.webdriver.common.by import By
    from selenium.common.exceptions import TimeoutException
    
    #### tkinter to ask for CSV File ####
    from tkinter import Tk
    from tkinter.filedialog import askopenfilename
    
    
    chrome_options = Options()
    chrome_options.add_argument("--user-data-dir=<PATH TO CHROME PROFILE>")
    
    # download the chrome driver from https://sites.google.com/a/chromium.org/chromedriver/downloads and put it in the
    # current directory
    
    service = Service('C:\\WebDriver\\bin\\chromedriver.exe')
    service.start()
    driver = webdriver.Remote(service.service_url, options=chrome_options)
    
    def setCodes(driver, code):
        editURL = "https://www.shoolu.com/manage/marketing/coupons/" + str(code)+"/edit"
        driver.get(editURL)
    
        element_present = EC.presence_of_element_located(
            (By.ID, "content-iframe"))
        WebDriverWait(driver, 5).until(element_present)
        driver.switch_to.frame(driver.find_element_by_id("content-iframe"))
        try:
            element_present = EC.presence_of_element_located(
                (By.ID, "excludeDiscounts"))
            WebDriverWait(driver, 5).until(element_present)
        finally:
            enable = driver.find_element_by_id("excludeDiscounts")
            print(enable.get_attribute("checked"))
            if enable.get_attribute("checked") != 'true':
                print("Checking Box")
                enable.send_keys(' ')
                driver.find_element_by_name("SaveButton1").click()
                WebDriverWait(driver, 5).until(
                    lambda driver: driver.current_url != editURL)
    
    
    #### LOG IN TO WEBSITE ####
    driver.get("https://shoolu.com/manage")
    try:
        username = driver.find_element_by_id("user_email")
        username.clear()
        username.send_keys("USERNAME")
    
        password = driver.find_element_by_id("user_password")
        password.clear()
        password.send_keys("PASSWORD")
        driver.find_element_by_name("commit").click()
    except:
        print("Already Logged In")
    
    #### GET CSV FILE OF CODE IDs ####
    Tk().withdraw()
    filename = askopenfilename() # Fetch File
    print(filename)
    
    with open(filename, 'r') as selectedFile:
        next(selectedFile) # Skip Header Row
        try:
            for row in selectedFile:
                rows = row.split(",") # Turn Each Row Into It's Own List
                print(rows[0])
    
                try:
                    setCodes(driver, rows[0])
                except:
                    print("Error Setting")
        finally:
            driver.quit() # Kill Browser Window After Everything is Done
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

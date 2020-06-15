---
title: plenarprotokollscraper
date: 2020-05-07
---
Example Python program plenarprotokollscraper.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import bs4
* import requests, re, collections, sys
* import urllib.request
* from urllib.parse import urljoin
* from PyQt5.QtWebEngineWidgets import QWebEnginePage
* from PyQt5.QtWidgets import QApplication
* from PyQt5.QtCore import QUrl
* from pymarkovchain import MarkovChain

## Classes

* class Rede:
* """ # class for scraping dynamic web-content without a browser:
* class Page(QWebEnginePage):  

## Methods

* def __init__(self, rednerID, fraktion, redeText, thema):
* def __repr__(self):
* def __init__(self, url):
* def _on_load_finished(self):
* def Callable(self, html_str):
* def makeHTMLSoup(url):
* def makeXMLSoup(url):
* def makeLXMLSoup(url):
* def get_speeches(link):
* def generate_speech(speechText, numOfLines):
* def main():

## Code

Example Python PyQt program :

    import bs4
    import requests, re, collections, sys
    import urllib.request
    from urllib.parse import urljoin
    from PyQt5.QtWebEngineWidgets import QWebEnginePage
    from PyQt5.QtWidgets import QApplication
    from PyQt5.QtCore import QUrl
    from pymarkovchain import MarkovChain
    
    startUrl = 'https://www.bundestag.de/services/opendata/';
    baseUrl = 'https://www.bundestag.de/'
    baseCaseXHRUrl = 'https://www.bundestag.de/ajax/filterlist/de/services/opendata/543410-543410/h_49f0d94cb26682ff1e9428b6de471a5b?limit=10&noFilterSet=true&offset='
    alleReden = []
    fraktion = "SPD"
    
    class Rede:
        def __init__(self, rednerID, fraktion, redeText, thema):
            self.rednerID = rednerID
            self.fraktion = fraktion
            self.redeText = redeText
            self.thema = thema
        def __repr__(self):
            return str("rednerID: " + self.rednerID + ", " + " fraktion: " + self.fraktion + ", ")
    
    """ # class for scraping dynamic web-content without a browser:
    class Page(QWebEnginePage):  
        def __init__(self, url):
            self.app = QApplication(sys.argv)
            QWebEnginePage.__init__(self)
            self.html = ''
            self.loadFinished.connect(self._on_load_finished)
            self.load(QUrl(url))
            self.app.exec_()
    
        def _on_load_finished(self):
            self.html = self.toHtml(self.Callable)
            print('Load finished')
    
        def Callable(self, html_str):
            self.html = html_str
            self.app.quit()
    
    
    def makeHTMLSoup(url):
        page = Page(url)
        soup = bs4.BeautifulSoup(page.html, 'html.parser')
        print(soup)
        return soup """
    
    def makeXMLSoup(url):
        r = requests.get(url)
        soup = bs4.BeautifulSoup(r.text, 'xml')
        return soup
    
    def makeLXMLSoup(url):
        r = requests.get(url)
        soup = bs4.BeautifulSoup(r.text, 'lxml')
        return soup
    
    def get_speeches(link):
        soup = makeXMLSoup(link)
        redenListe = []
        speeches = []
        speeches = soup.find_all('rede')
        #f = open("speeches.txt", "a", encoding="utf-8")
        for speech in speeches:
            currSpeech = speech.find_all('p', {'klasse':re.compile('J|J_1')})
            currSpeechText = ""
            for allText in currSpeech:
                #if allText.find('name', text ='Präsident Dr. Wolfgang Schäuble:' | text='Vizepräsidentin Petra Pau:').extract.next_sibling
                print(allText.text)
                #print(allText.text, file=f) 
                currSpeechText += allText.text
            fraktion = speech.find('fraktion')
            if fraktion:
                fraktion = fraktion.text
            else:
                fraktion = ''
            rede = Rede(speech.redner["id"], fraktion, currSpeechText, "")
            redenListe.append(rede)
        #f.close()
        alleReden.extend(redenListe)
    
    def generate_speech(speechText, numOfLines):
        # Generate a Markov model
        mc = MarkovChain("./markov")
        mc.generateDatabase(speechText)
        result = []
        for line in range(0, numOfLines):
            result.append(mc.generateString())
        print(result)
    
    
    def main():
        maxOffset = 150
        offsetStep = 10
        for offset in range(0, maxOffset, offsetStep): 
            currentUrl = baseCaseXHRUrl + str(offset)  
            soup = makeLXMLSoup(currentUrl)
            tags = []
            for tag in soup.find_all('a', href=re.compile(r'/resource/blob/.*-data.xml')):
                tags.append(tag)
            links = [urljoin(baseUrl, a['href'])for a in tags]  # convert relative url to absolute url
            for link in links:
                get_speeches(link)
        speechText = ""
        for rede in alleReden:
            if rede.fraktion == "AfD":
                speechText += rede.redeText + " "
        generate_speech(speechText, 100)
    
    if __name__ == '__main__': main()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

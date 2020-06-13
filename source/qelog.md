---
title: qelog
date: 2020-05-07
---
Example Python program qelog.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import string
* import sys
* import re
* from PyQt5.QtCore import QByteArray, QUrl
* from PyQt5.QtGui import QFont, QTextDocument
* from PyQt5.QtNetwork import QNetworkAccessManager, QNetworkRequest
* from PyQt5.QtWidgets import *
* from PyQt5.QtWebEngineWidgets import QWebEngineView, QWebEngineProfile

## Methods

* def urlChangedCallback(url):
* def tryLoadElog(elogId):
* def tryLoadElogCatTree():
* def printLoadedElog():
* def addNodeToSubTree(subTree, path, value):
* def addTreeToItem(item, tree):
* def printLoadedCatList():

## Code

Example Python PyQt program :

    #! /usr/bin/env python3
    
    import string
    import sys
    import re
    
    from PyQt5.QtCore import QByteArray, QUrl
    from PyQt5.QtGui import QFont, QTextDocument
    from PyQt5.QtNetwork import QNetworkAccessManager, QNetworkRequest
    from PyQt5.QtWidgets import *
    from PyQt5.QtWebEngineWidgets import QWebEngineView, QWebEngineProfile
    
    loginPageUrl = QUrl('https://cmsonline.cern.ch/cms-elog/1')
    
    def urlChangedCallback(url):
        global loggingIn
        if url.host() == 'login.cern.ch':
            print('>>>', 'Logging in')
            loggingIn = True
        elif loggingIn and url.host() != 'login.cern.ch':
            dialog.accept()
            tryLoadElogCatTree()
            #tryLoadElog(1)
            loggingIn = False
        else:
            print('>>>', url.host(), url.toEncoded())
    
    def tryLoadElog(elogId):
        url = 'https://cmsonline.cern.ch/cms-elog/%d'
        request = QNetworkRequest(QUrl(url % elogId))
        request.setAttribute(QNetworkRequest.FollowRedirectsAttribute, True)
        request.setRawHeader(b'Accept', b'*/*')
        request.setRawHeader(b'User-Agent', b'qelog 0.0')
        global reply
        reply = manager.get(request)
        reply.finished.connect(printLoadedElog)
        window.setWindowTitle('elog #%d \uff0d qelog' % elogId)
    
    def tryLoadElogCatTree():
        url = 'https://cmsonline.cern.ch/webcenter/portal/cmsonline/pages_common/elog?_piref623564097.strutsAction=%2Frss.do%3FsubId%3D30'
        request = QNetworkRequest(QUrl(url))
        request.setAttribute(QNetworkRequest.FollowRedirectsAttribute, True)
        request.setRawHeader(b'Accept', b'*/*')
        request.setRawHeader(b'User-Agent', b'qelog 0.0')
        global reply
        reply = manager.get(request)
        reply.finished.connect(printLoadedCatList)
    
    def printLoadedElog():
        print('>>> ', reply.url())
        print('>>> ',
              reply.attribute(QNetworkRequest.HttpStatusCodeAttribute),
              reply.attribute(QNetworkRequest.HttpReasonPhraseAttribute))
        contentType = reply.header(QNetworkRequest.ContentTypeHeader)
        charset = contentType.split(r'=')[1]
        html = bytes(reply.readAll()).decode(charset)
    
        regex = re.compile('<tr><td><pre class="messageprefull">(.*)</pre></td></tr>',
                           re.DOTALL | re.UNICODE)
        match = re.search(regex, html)
        if match is None:
            print('No elog found :\'(')
            sys.exit(1)
        else:
            document = QTextDocument(match.group(1), edit)
            document.setDefaultFont(font)
            document.setDocumentLayout(QPlainTextDocumentLayout(document))
            edit.setDocument(document)
    
    def addNodeToSubTree(subTree, path, value):
        name = path[0]
        if not (name in subTree):
            subTree[name] = {} if len(path) > 1 else value
        if len(path) > 1:
            addNodeToSubTree(subTree[name], path[1:], value)
    
    def addTreeToItem(item, tree):
        if type(tree) == dict:
            for name, subTree in tree.items():
                subItem = QTreeWidgetItem([name])
                addTreeToItem(subItem, subTree)
                item.addChild(subItem)
        else:
            item.addChild(QTreeWidgetItem([str(tree)]))
    
    def printLoadedCatList():
        print('>>> ', reply.url())
        print('>>> ',
              reply.attribute(QNetworkRequest.HttpStatusCodeAttribute),
              reply.attribute(QNetworkRequest.HttpReasonPhraseAttribute))
        contentType = reply.header(QNetworkRequest.ContentTypeHeader)
        charset = contentType.split(r'=')[1]
        html = bytes(reply.readAll()).decode(charset)
    
        regex = re.compile(r'feeds.jsp\?sd=([0-9]+)&msgUrl=.*?><img.*?>(.*?)</a>',
                           re.DOTALL | re.UNICODE)
    
        tree = {}
        for match in re.finditer(regex, html):
            id = int(match.group(1))
            path = [ s.strip() for s in match.group(2).split('>') ]
            addNodeToSubTree(tree, path, id)
    
        topLevel = QTreeWidgetItem()
        addTreeToItem(topLevel, tree)
        for child in topLevel.takeChildren():
            treeWidget.addTopLevelItem(child)
    
        print(tree)
    
    app = QApplication([])
    
    font = QFont('Monospace')
    font.setStyleHint(QFont.TypeWriter);
    
    treeWidget = QTreeWidget()
    
    edit = QPlainTextEdit()
    edit.setReadOnly(True)
    
    splitter = QSplitter()
    splitter.addWidget(treeWidget)
    splitter.addWidget(edit)
    
    window = QMainWindow()
    window.setCentralWidget(splitter)
    window.resize(1000, 800)
    window.show()
    
    manager = QNetworkAccessManager()
    
    loggingIn = False
    
    profile = QWebEngineProfile.defaultProfile()
    cookieStore = profile.cookieStore()
    cookieStore.cookieAdded.connect(manager.cookieJar().insertCookie)
    cookieStore.cookieRemoved.connect(manager.cookieJar().deleteCookie)
    
    webView = QWebEngineView()
    webView.load(loginPageUrl)
    webView.setSizePolicy(QSizePolicy(QSizePolicy.Expanding, QSizePolicy.Expanding))
    webView.urlChanged.connect(urlChangedCallback)
    
    layout = QVBoxLayout()
    layout.setContentsMargins(0, 0, 0, 0)
    layout.addWidget(webView)
    
    dialog = QDialog(window)
    dialog.setWindowTitle('Log in to your CERN account')
    dialog.setLayout(layout)
    dialog.setModal(True)
    dialog.resize(700, 500)
    dialog.exec()
    
    app.exec_()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

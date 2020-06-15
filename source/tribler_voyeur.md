---
title: tribler_voyeur
date: 2020-05-07
---
Example Python program tribler_voyeur.py
This program creates a PyQt GUI
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* from collections import OrderedDict
* from datetime import datetime
* from json import loads
* from sys import argv, exit, stderr
* from threading import Thread
* from time import mktime, sleep
* from urllib2 import urlopen
* import PyQt5
* from PyQt5.QtWidgets import QWidget, QApplication, QListWidget, QAbstractItemView, QListWidgetItem, QGridLayout
* from PyQt5.QtGui import QPixmap, QIcon
* from PyQt5.QtCore import QSize, Qt

## Classes

* class ListWidgetItem(QListWidgetItem):
* class FeedListener(Thread):
* class TriblerFeedWindow(QWidget):

## Methods

* def __init__(self, icon, text, timestamp):
* def __lt__(self, other):
* def __init__(self, feed_window):
* def end(self):
* def update_feed(self, new_keys):
* def run(self):
* def __init__(self):
* def load_window_icon(self):
* def add_components(self):
* def update_list(self, items):
* def load_image_from_url(self, url, text, timestamp):
* def closeEvent(self, event):

## Code

Example Python PyQt program :

    #!/usr/bin/python2
    """
    This script opens a window in which all recent events from the Tribler
    organisation on GitHub are displayed.
    
    Requires PyQt5 to be installed!
    """
    
    from collections import OrderedDict
    from datetime import datetime
    from json import loads
    from sys import argv, exit, stderr
    from threading import Thread
    from time import mktime, sleep
    from urllib2 import urlopen
    
    try:
        import PyQt5
    except ImportError:
        print "You do not appear to have PyQt5 installed! Shutting down :("
        exit(1)
    
    from PyQt5.QtWidgets import QWidget, QApplication, QListWidget, QAbstractItemView, QListWidgetItem, QGridLayout
    from PyQt5.QtGui import QPixmap, QIcon
    from PyQt5.QtCore import QSize, Qt
    
    
    class ListWidgetItem(QListWidgetItem):
    
        """
        Sortable list item: QListWidgetItem + timestamp
        """
    
        def __init__(self, icon, text, timestamp):
            super(ListWidgetItem, self).__init__(icon, text)
            self.timestamp = timestamp
    
        def __lt__(self, other):
            return self.timestamp < other.timestamp
    
    
    class FeedListener(Thread):
    
        """
        Thread pulling info from GitHub every minute.
        """
    
        def __init__(self, feed_window):
            super(FeedListener, self).__init__()
            self.feed_window = feed_window
            self.running = True
            self.feed = OrderedDict()
    
        def end(self):
            self.running = False
    
        def update_feed(self, new_keys):
            items = []
            num = 0
            for key in new_keys:
                avatar_url, user_name, event_name, repo = self.feed[key]
                repo = repo[repo.index('/')+1:]
                # Convert utc to local time
                utc = datetime.strptime(key, '%Y-%m-%dT%H:%M:%SZ')
                epoch = mktime(utc.timetuple())
                offset = datetime.fromtimestamp(epoch) - datetime.utcfromtimestamp(epoch)
                local_time = str(utc + offset)
                # Construct message
                joiner = "an" if event_name[0].lower() in ['a', 'e', 'i', 'o', 'u'] else "a"
                text = "[" + repo + "][" + local_time + "] " + user_name + " caused " + joiner + " " + event_name + "!"
                items.append(self.feed_window.load_image_from_url(avatar_url, text, key))
    
                num += 1
                if num == MAX_ITEMS:
                    break
            self.feed_window.update_list(items)
    
        def run(self):
            while self.running:
                try:
                    data = urlopen("https://api.github.com/orgs/Tribler/events").read()
                    objects = loads(data)
    
                    new_keys = []
    
                    for object in objects:
                        key = object["created_at"]
                        if key not in self.feed:
                            self.feed[key] = (object["actor"]["avatar_url"],
                                              object["actor"]["display_login"],
                                              object["type"],
                                              object["repo"]["name"])
                            new_keys.append(key)
    
                    self.update_feed(new_keys)
    
                    if len(self.feed.keys()) > 2*MAX_ITEMS:
                        for key in reversed(self.feed):
                            self.feed.pop(key, None)
                except Exception as e:
                    print >> stderr, e
    
                for i in xrange(60):
                    if self.running:
                        sleep(1)
                    else:
                        break
    
    
    class TriblerFeedWindow(QWidget):
    
        """
        Qt Window displaying the events in a list
        """
        
        def __init__(self):
            super(TriblerFeedWindow, self).__init__()
    
            self.setWindowTitle('Tribler Feed')
            self.load_window_icon()
            self.add_components()
            self.showMaximized()
    
            self.first_load = True
            self.icon_cache = {}
    
            self.feed_listener = FeedListener(self)
            self.feed_listener.start()
    
        def load_window_icon(self):
            try:
                data = urlopen("https://tribler.org/img/anonymity.png").read()
                pixmap = QPixmap()
                pixmap.loadFromData(data)
                self.setWindowIcon(QIcon(pixmap))
            except:
                pass
    
        def add_components(self):
            self.item_list = QListWidget(self)
            self.item_list.setSelectionMode(QAbstractItemView.NoSelection)
            self.item_list.setAlternatingRowColors(True)
            self.item_list.addItems(["Loading...",])
            self.item_list.show()
    
            grid = QGridLayout()
            grid.addWidget(self.item_list)
            self.setLayout(grid)
    
        def update_list(self, items):
            if self.first_load:
                self.item_list.clear()
                self.first_load = False
    
            rect = self.item_list.geometry()
            total_items = self.item_list.count() + len(items)
            height = max(min((rect.height())/min(MAX_ITEMS, total_items + len(items)), 100), 10)
    
            for item in items:
                item.setSizeHint(QSize(0, height))
                self.item_list.addItem(item)
    
            self.item_list.sortItems(Qt.DescendingOrder)
            if total_items > MAX_ITEMS:
                for i in range(total_items - MAX_ITEMS):
                    self.item_list.takeItem(total_items - i)
    
        def load_image_from_url(self, url, text, timestamp):
            if url in self.icon_cache:
                icon = self.icon_cache[url]
            else:
                data = urlopen(url).read()
                pixmap = QPixmap()
                pixmap.loadFromData(data)
                icon = QIcon(pixmap)
                self.icon_cache[url] = icon
            return ListWidgetItem(icon, text, timestamp)
            
        def closeEvent(self, event):
            self.feed_listener.end()
            
            
    if __name__ == '__main__':
        app = QApplication(argv)
        MAX_ITEMS = app.primaryScreen().size().height()/30
        ex = TriblerFeedWindow()
        exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

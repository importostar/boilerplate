---
title: tribler_request_manager
date: 2020-05-07
---
Example Python program tribler_request_manager.py

## Modules

* import json
* import logging
* import random
* import string
* from time import time
* from PyQt5.QtCore import QUrl, pyqtSignal, QIODevice, QBuffer
* from PyQt5.QtNetwork import QNetworkAccessManager, QNetworkRequest

## Classes

* class TriblerRequestManager(QNetworkAccessManager):
* :param capture_errors: whether errors should be handled by this class (defaults to True)

## Methods

* def __init__(self):
* def generate_request_id(self):
* def perform_request(self, url, read_callback, data="", method='GET', capture_errors=True):
* def get_message_from_error(error):
* def on_finished(self, reply, capture_errors):
* def download_file(self, endpoint, read_callback):
* def on_file_download_finished(self, reply):
* def cancel_request(self):

## Code

Example Python PyQt program :

    import json
    import logging
    import random
    import string
    from time import time
    
    from PyQt5.QtCore import QUrl, pyqtSignal, QIODevice, QBuffer
    from PyQt5.QtNetwork import QNetworkAccessManager, QNetworkRequest
    
    performed_requests = {}
    performed_requests_ids = []
    
    
    class TriblerRequestManager(QNetworkAccessManager):
        """
        This class is responsible for all the requests made to the Tribler REST API.
        """
        window = None
    
        received_json = pyqtSignal(object, int)
        received_file = pyqtSignal(object)
    
        def __init__(self):
            QNetworkAccessManager.__init__(self)
            self.request_id = None
            self.reply = None
            self.generate_request_id()
    
        def generate_request_id(self):
            self.request_id = ''.join(random.choice(string.ascii_uppercase + string.digits) for _ in range(10))
    
        def perform_request(self, url, read_callback, data="", method='GET', capture_errors=True):
            """
            Perform a HTTP request.
            :param endpoint: the endpoint to call (i.e. "statistics")
            :param read_callback: the callback to be called with result info when we have the data
            :param data: optional POST data to be sent with the request
            :param method: the HTTP verb (GET/POST/PUT/PATCH)
            :param capture_errors: whether errors should be handled by this class (defaults to True)
            """
            performed_requests[self.request_id] = [url, method, data, time(), -1]
            performed_requests_ids.append(self.request_id)
            if len(performed_requests_ids) > 200:
                del performed_requests[performed_requests_ids.pop(0)]
    
            if method == 'GET':
                buf = QBuffer()
                buf.setData(data)
                buf.open(QIODevice.ReadOnly)
                get_request = QNetworkRequest(QUrl(url))
                self.reply = self.sendCustomRequest(get_request, "GET", buf)
                buf.setParent(self.reply)
            elif method == 'PATCH':
                buf = QBuffer()
                buf.setData(data)
                buf.open(QIODevice.ReadOnly)
                patch_request = QNetworkRequest(QUrl(url))
                self.reply = self.sendCustomRequest(patch_request, "PATCH", buf)
                buf.setParent(self.reply)
            elif method == 'PUT':
                request = QNetworkRequest(QUrl(url))
                request.setHeader(QNetworkRequest.ContentTypeHeader, "application/x-www-form-urlencoded")
                self.reply = self.put(request, data)
            elif method == 'DELETE':
                buf = QBuffer()
                buf.setData(data)
                buf.open(QIODevice.ReadOnly)
                delete_request = QNetworkRequest(QUrl(url))
                self.reply = self.sendCustomRequest(delete_request, "DELETE", buf)
                buf.setParent(self.reply)
            elif method == 'POST':
                request = QNetworkRequest(QUrl(url))
                request.setHeader(QNetworkRequest.ContentTypeHeader, "application/x-www-form-urlencoded")
                self.reply = self.post(request, data)
    
            if read_callback:
                self.received_json.connect(read_callback)
    
            self.finished.connect(lambda reply: self.on_finished(reply, capture_errors))
    
        @staticmethod
        def get_message_from_error(error):
            return_error = None
            if isinstance(error['error'], (str, unicode)):
                return_error = error['error']
            elif 'message' in error['error']:
                return_error = error['error']['message']
    
            if not return_error:
                return json.dumps(error)  # Just print the json object
            return return_error
    
        def on_finished(self, reply, capture_errors):
            status_code = reply.attribute(QNetworkRequest.HttpStatusCodeAttribute)
            if not reply.isOpen() or not status_code:
                self.received_json.emit(None, reply.error())
                return
    
            performed_requests[self.request_id][4] = status_code
    
            data = reply.readAll()
            try:
                json_result = json.loads(str(data), encoding='latin_1')
    
                if 'error' in json_result and capture_errors:
                    pass
                    #self.show_error(TriblerRequestManager.get_message_from_error(json_result))
                else:
                    self.received_json.emit(json_result, reply.error())
            except ValueError:
                self.received_json.emit(None, reply.error())
                logging.error("No json object could be decoded from data: %s" % data)
    
            # We disconnect the slot since we want the finished only to be emitted once. This allows us to reuse the
            # request manager.
            try:
                self.finished.disconnect()
                self.received_json.disconnect()
            except TypeError:
                pass  # We probably didn't have any connected slots.
    
        def download_file(self, endpoint, read_callback):
            url = self.base_url + endpoint
            self.reply = self.get(QNetworkRequest(QUrl(url)))
            self.received_file.connect(read_callback)
            self.finished.connect(self.on_file_download_finished)
    
        def on_file_download_finished(self, reply):
            data = reply.readAll()
            self.received_file.emit(data)
    
        def cancel_request(self):
            if self.reply:
                self.reply.abort()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

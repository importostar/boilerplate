---
title: Server
date: 2020-05-07
---
Example Python program Server.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from socket import AF_INET, socket, SOCK_STREAM
* from threading import Thread
* import threading

## Methods

* def accept_incoming_connections():
* def handle_client(client):  # Takes client socket as argument.
* def broadcast(msg, prefix=""):  # prefix is for name identification.

## Code

Python example

    """Server for multithreaded (asynchronous) chat application."""
    from socket import AF_INET, socket, SOCK_STREAM
    from threading import Thread
    import threading
    
    
    def accept_incoming_connections():
        """Sets up handling for incoming clients."""
        while True:
                client, client_address = SERVER.accept()
                print("%s:%s has connected." % client_address)
                welcome1 = "Please Enter your username."
                client.send(bytes(welcome1, "utf8"))
                addresses[client] = client_address
                Thread(target=handle_client, args=(client,)).start()
    
    
    def handle_client(client):  # Takes client socket as argument.
        """Handles a single client connection."""
    
        name = client.recv(BUFSIZ).decode("utf8")
        welcome1 = 'Welcome to the server %s!' % name
        welcome2 = 'If you ever want to quit, type {quit} to exit.'
        client.send(bytes(welcome1, "utf8"))
        client.send(bytes(welcome2, "utf-8"))
        msg = " has joined the chat!"
        print(f"{name} has joined...")
        broadcast(bytes(msg, "utf8"), name)
        clients[client] = name
    
        while True:
            msg = client.recv(BUFSIZ)
            if msg != bytes("{quit}", "utf8"):
                broadcast(msg, name+" -----> ")
                norm_message = msg.decode("utf8")
                print(f"{name} has '{norm_message}' sent to all users...")
            else:
                try:
                    client.send(bytes("{quit}", "utf8"))
                    client.close()
                    del clients[client]
                    print(name, "has disconnected from the server...")
                    broadcast(bytes("%s has left the chat." % name, "utf8"))
                    break
                except Exception:
                    break
    
    
    def broadcast(msg, prefix=""):  # prefix is for name identification.
        """Broadcasts a message to all the clients."""
        try:
            for sock in clients:
                sock.send(bytes(prefix, "utf8")+msg)
        except Exception as e:
            print(e)
    
    
    clients = {}
    addresses = {}
    
    HOST = "Josh-PC"
    PORT = 9050
    BUFSIZ = 1024
    ADDR = (HOST, PORT)
    
    SERVER = socket(AF_INET, SOCK_STREAM)
    
    if __name__ == "__main__":
        try:
            SERVER.listen(5)
            print("Server Starting...")
            print("Server Started...")
            print("Waiting for connection...")
            ACCEPT_THREAD = Thread(target=accept_incoming_connections)
            ACCEPT_THREAD.start()
            ACCEPT_THREAD.join()
            SERVER.close()
        except Exception:
            print("SERVER ERROR: 101")

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

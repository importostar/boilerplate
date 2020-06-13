---
title: sshclient
date: 2020-05-07
---
Example Python program sshclient.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* # import python modules
* from socket import *

## Code

Python example

    #!/usr/bin/python
    # import python modules
    from socket import *
    HOST = '67.21.78.234'      # '' means bind to all interfaces
    PORT = 9090    #  port
    # create our socket handler
    s = socket(AF_INET, SOCK_STREAM)
    #  when canceled out we can reuse port
    s.setsockopt(SOL_SOCKET, SO_REUSEADDR, 1)
    # bind to interface
    s.bind((HOST, PORT))
    # print we are accepting connections
    print "Listening on 0.0.0.0:%s" % str(PORT)
    # listen for only 10 connection
    s.listen(10)
    # accept connections
    conn, addr = s.accept()
    # print connected by ipaddress
    print 'Connected by', addr
    # receive initial connection
    data = conn.recv(1024)
    # start loop
    while 1:
         # enter shell command
         command = raw_input("Enter shell command or quit: ")
         # send shell command
         conn.send(command)
         # if we specify quit then break out of loop and close socket
         if command == "quit": break
         # receive output from linux command
         data = conn.recv(1024)
         # print the output of the linux command
         print data
    # close socket
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

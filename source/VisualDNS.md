---
title: VisualDNS
date: 2020-05-07
---
Example Python program VisualDNS.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import socket  # Used for DNS functions
* import tkinter  # Used to create GUI
* import re  # Used for regex functions
* import pyperclip  # Used for clipboard functions

## Classes

* class DnsGetter:

## Methods

* def __init__(self):
* def _get_host() -> str:
* def _host_type(_host) -> bool:
* def _by_ip(_host) -> str:
* def _by_name(_host) -> str:
* def main_window(_host):
* def resolve(self, _host):
* def main():

## Code

Python tkinter example

    import socket  # Used for DNS functions
    import tkinter  # Used to create GUI
    import re  # Used for regex functions
    import pyperclip  # Used for clipboard functions
    
    
    class DnsGetter:
        """Resolves an IP or Name and displays the result in a window along with copying the result to the clip board."""
    
        def __init__(self):
            self._host = self._get_host()  # Get host or IP from the clipboard
            self.resolve(self._host)  # Main function
    
        @staticmethod
        def _get_host() -> str:
            """Gets the host or IP from the clip board"""
            return pyperclip.paste()
    
        @staticmethod
        def _host_type(_host) -> bool:
            """Check to see if it is an IP of a host name.
             Returns a bool True if it is a host name and bool False if it is an IP"""
            _result = re.match("[a-z]", _host.lower())
            if _result:
                return True  # Regex had a match to characters a-z
            else:
                return False  # Regex had no match to characters a-z
    
        @staticmethod
        def _by_ip(_host) -> str:
            """Resolves an IP to DNS name and returns the result as a string"""
    
            try:
                name = socket.gethostbyaddr(_host)
                return name[0]  # socket.gethostbyaddr returns a tuple with 3 items.  We only want the first one[0].
    
            except socket.error:
                return "IP could not be resolved to a name"
    
        @staticmethod
        def _by_name(_host) -> str:
            """Resolves a name to IP amd returns the result as a string"""
            try:
                ip = socket.gethostbyname(_host)
                return ip
    
            except socket.error:
                return "Could not resolve the name to an IP address"
    
        @staticmethod
        def main_window(_host):
            """Creates GUI window to display result in"""
            window = tkinter.Tk()
            window.title("DNS Getter")
            window.geometry("200x50+4+400")  # Set window size
            label = tkinter.Label(window, text=_host)
            label.pack(side="top")
            window.after(5000, lambda: window.destroy())  # Close GUI after 5 seconds
            window.mainloop()  # Loop until window is closed or timer runs out.
    
        def resolve(self, _host):
            """Main function for resolving IPs or host names"""
            if self._host_type(_host):  # Depending on if the data from the clip board
                                        # is an IP or a name we need to call the correct function to resolve it.
                result = self._by_name(_host)
            else:
                result = self._by_ip(_host)
            print(''.join(str(result)))
            pyperclip.copy(''.join(str(result)))  # Copy result to the clipboard
            self.main_window(result)
    
    
    def main():
        """Main Function"""
        DnsGetter()
    
    
    if __name__ == '__main__':  # Check if we are executing directly from this file
        main()
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: pyConversor
date: 2020-05-07
---
Example Python program pyConversor.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import ipaddress
* import tkinter
* import tkinter.ttk
* import tkinter.messagebox
* import sys

## Classes

* class MainWindow():

## Methods

* def bin2dec(value):
* def bin2hex(value):
* def dec2bin(value):
* def dec2hex(value):
* def hex2bin(value):
* def hex2dec(value):
* def ip2int(value):
* def int2ip(value):
* 	def __init__(self):
* 	def evt_bt_bin(self):
* 	def evt_bt_dec(self):
* 	def evt_bt_hex(self):
* 	def evt_bt_ip(self):
* 	def _set_values(self, bin_value, dec_value, hex_value, ip_value):
* 	def mainloop(self):

## Code

Python tkinter example

    #!/usr/bin/env python3
    
    import ipaddress
    import tkinter
    import tkinter.ttk
    import tkinter.messagebox
    import sys
    
    
    def bin2dec(value):
    	return int(value, 2)
    
    def bin2hex(value):
    	return hex(int(value, 2))
    
    def dec2bin(value):
    	return bin(int(value))
    
    def dec2hex(value):
    	return hex(int(value))
    
    def hex2bin(value):
    	return bin(int(value, 16))
    
    def hex2dec(value):
    	return int(value, 16)
    
    def ip2int(value):
    	return int(ipaddress.IPv4Address(str(value)))
    
    def int2ip(value):
    	return str(ipaddress.IPv4Address(int(value)))
    
    
    class MainWindow():
    	
    	C_FONT = ("Consolas", 16)
    	C_TXT_MAXLEN = 32
    	
    	def __init__(self):
    		self._window = tkinter.Tk()
    		self._window.title("    pyConversor    ")
    		self._window.geometry("820x260")
    		self._window.resizable(False, False)
    		
    		label = tkinter.Label(self._window, text="Number: ", font=MainWindow.C_FONT)
    		label.grid(row=0, column=0, padx=10, pady=5)
    		
    		self._txt_input = tkinter.Entry(self._window, width=MainWindow.C_TXT_MAXLEN, font=MainWindow.C_FONT)
    		self._txt_input.grid(row=0, column=1, pady=5)
    		self._txt_input.focus()
    		
    		self._bt_bin = tkinter.Button(self._window, text="Bin", font=MainWindow.C_FONT, command=self.evt_bt_bin)
    		self._bt_bin.grid(row=0, column=2, padx=5, pady=5)
    		
    		self._bt_dec = tkinter.Button(self._window, text="Dec", font=MainWindow.C_FONT, command=self.evt_bt_dec)
    		self._bt_dec.grid(row=0, column=4, padx=5, pady=5)
    		
    		self._bt_hex = tkinter.Button(self._window, text="Hex", font=MainWindow.C_FONT, command=self.evt_bt_hex)
    		self._bt_hex.grid(row=0, column=6, padx=5, pady=5)
    		
    		self._bt_ip = tkinter.Button(self._window, text="IP", font=MainWindow.C_FONT, command=self.evt_bt_ip)
    		self._bt_ip.grid(row=0, column=8, padx=5, pady=5)
    		
    		separator = tkinter.ttk.Separator(self._window,orient=tkinter.HORIZONTAL)
    		separator.grid(row=1, column=1, pady=10)
    		
    		label = tkinter.Label(self._window, text="Binary:", font=MainWindow.C_FONT)
    		label.grid(row=2, column=0,  padx=10, pady=5)
    		
    		self._stringvar_bin = tkinter.StringVar()
    		txt_output = tkinter.Entry(self._window, textvariable=self._stringvar_bin, width=MainWindow.C_TXT_MAXLEN, state="readonly", font=MainWindow.C_FONT)
    		txt_output.grid(row=2, column=1, pady=5)
    		
    		label = tkinter.Label(self._window, text="Decimal:", font=MainWindow.C_FONT)
    		label.grid(row=3, column=0,  padx=10, pady=5)
    		
    		self._stringvar_dec = tkinter.StringVar()
    		txt_output = tkinter.Entry(self._window, textvariable=self._stringvar_dec, width=MainWindow.C_TXT_MAXLEN, state="readonly", font=MainWindow.C_FONT)
    		txt_output.grid(row=3, column=1, pady=5)
    		
    		label = tkinter.Label(self._window, text="Hexadecimal:", font=MainWindow.C_FONT)
    		label.grid(row=4, column=0,  padx=10, pady=5)
    		
    		self._stringvar_hex = tkinter.StringVar()
    		txt_output = tkinter.Entry(self._window, textvariable=self._stringvar_hex, width=MainWindow.C_TXT_MAXLEN, state="readonly", font=MainWindow.C_FONT)
    		txt_output.grid(row=4, column=1, pady=5)
    		
    		label = tkinter.Label(self._window, text="IP Address:", font=MainWindow.C_FONT)
    		label.grid(row=5, column=0,  padx=10, pady=5)
    		
    		self._stringvar_ip = tkinter.StringVar()
    		txt_output = tkinter.Entry(self._window, textvariable=self._stringvar_ip, width=MainWindow.C_TXT_MAXLEN, state="readonly", font=MainWindow.C_FONT)
    		txt_output.grid(row=5, column=1, pady=5)
    		
    	def evt_bt_bin(self):
    		try:
    			bin_value = self._txt_input.get().strip().replace(" ", "")
    			dec_value = bin2dec(bin_value)
    			hex_value = bin2hex(bin_value)
    			ip_value = int2ip(dec_value)
    			
    			self._set_values(bin_value, dec_value, hex_value, ip_value)
    			
    		except Exception:
    			tkinter.messagebox.showerror("Error", "Invalid conversion")
    			print(ex, file=sys.stderr)
    	
    	def evt_bt_dec(self):
    		try:
    			dec_value = self._txt_input.get().strip().replace(" ", "")
    			bin_value = dec2bin(dec_value)
    			hex_value = dec2hex(dec_value)
    			ip_value = int2ip(dec_value)
    			
    			self._set_values(bin_value, dec_value, hex_value, ip_value)
    			
    		except Exception as ex:
    			tkinter.messagebox.showerror("Error", "Invalid conversion")
    			print(ex, file=sys.stderr)
    		
    	def evt_bt_hex(self):
    		try:
    			hex_value = self._txt_input.get().strip().replace(" ", "")
    			bin_value = hex2bin(hex_value)
    			dec_value = hex2dec(hex_value)
    			ip_value = int2ip(dec_value)
    			
    			self._set_values(bin_value, dec_value, hex_value, ip_value)
    		
    		except Exception as ex:
    			tkinter.messagebox.showerror("Error", "Invalid conversion")
    			print(ex, file=sys.stderr)
    	
    	def evt_bt_ip(self):
    		try:
    			ip_value = self._txt_input.get().strip().replace(" ", "")
    			dec_value = ip2int(ip_value)
    			bin_value = dec2bin(dec_value)
    			hex_value = dec2hex(dec_value)
    			
    			self._set_values(bin_value, dec_value, hex_value, ip_value)
    		
    		except Exception as ex:
    			tkinter.messagebox.showerror("Error", "Invalid conversion")
    			print(ex, file=sys.stderr)
    	
    	def _set_values(self, bin_value, dec_value, hex_value, ip_value):
    		if not bin_value.startswith("0b"):
    			bin_value = "0b" + bin_value
    		if not hex_value.startswith("0x"):
    			hex_value = "0x" + hex_value
    		
    		self._stringvar_bin.set(bin_value)
    		self._stringvar_dec.set(dec_value)
    		self._stringvar_hex.set(hex_value)
    		self._stringvar_ip.set(ip_value)
    	
    	def mainloop(self):
    		self._window.mainloop()
    
    
    if __name__ == "__main__":
    	win = MainWindow()
    	win.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

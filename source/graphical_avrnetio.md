---
title: graphical_avrnetio
date: 2020-05-07
---
Example Python program graphical_avrnetio.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import time
* import telnetlib
* import Tkinter

## Methods

* def sg(netio, cmd):
* def version(netio): 
* def ipparams(netio):
* def adcs(netio):
* def adc(netio,i):
* def getads(netio):
* def Exit():
* def logtoggle():
* def toggle1(): sg(netio,'setport 1.' + ('1' if Output[0]['bg'] == color_off_bg else '0') ) #einschalten
* def toggle2(): sg(netio,'setport 2.' + ('1' if Output[1]['bg'] == color_off_bg else '0') ) #einschalten
* def toggle3(): sg(netio,'setport 3.' + ('1' if Output[2]['bg'] == color_off_bg else '0') ) #einschalten
* def toggle4(): sg(netio,'setport 4.' + ('1' if Output[3]['bg'] == color_off_bg else '0') ) #einschalten
* def toggle5(): sg(netio,'setport 5.' + ('1' if Output[4]['bg'] == color_off_bg else '0') ) #einschalten
* def toggle6(): sg(netio,'setport 6.' + ('1' if Output[5]['bg'] == color_off_bg else '0') ) #einschalten
* def toggle7(): sg(netio,'setport 7.' + ('1' if Output[6]['bg'] == color_off_bg else '0') ) #einschalten
* def toggle8(): sg(netio,'setport 8.' + ('1' if Output[7]['bg'] == color_off_bg else '0') ) #einschalten

## Code

Python tkinter example

    #!/usr/bin/python
    #-*- coding:utf8 -*-
    
    #=======================================================
    
    #    Connecting to AVR NET-IO with python
    #       with a graphical user interface
    
    #=======================================================
    # Funktionen:
    #+ Grafische Benutzerschnittstelle für AVR NET-IO "out of the box"
    #+ Auslesen und Anzeige aller verfügbaren Eingänge und Schalten der Ausgänge mit Schaltflächen
    #+ Zugriff über LAN (mit Telnet)
    #+ Logging aller Werte mit Timestamp in Logfile, kann mit Schaltfläche gestartet und gestoppt werden
    #+ Option: Logfile zum Anhängen geöffnet lassen / bei jedem Loggen neu öffnen
    
    #TODO: Diese Software ist noch ziemlich ausbaufähig:
    #- Anzeige von Firmwareversion und Verbindungsdaten (inkl. Port und MAC)
    #- Logfile-Optionen: Bei jedem Log-Start neue Datei beginnen mit Timestamp/Nummerierung / Überschreiben (Warnen) / Fortsetzen
    #- Preprend file info as comments at beginning of logfile if newly started
    #- Button "Logfile schließen und neu beginnen" (mit neuem Dateinamen/oder nicht, je nach Überschreibmodus)
    #- Festwert-Buttons für Abfrageintervall
    #- Abfrageintervall genauer machen (time.time()-Abfrage zum Auf-Feste-Sekunden-Legen, gemessene Korrektur (s.u.), Zeitgeber...
    #- count errors
    #- Different interface size: small, normal
    #- class version (enable controlling several devices)
    #- color selectors
    #- .rc file for saving configuration
    #- Lineare und andere Transformationsfunktionen für ADC-Werte
    #- Transport: Seriell, Telnet, TCP/IP, I2C, CAN, USB, Andere, ...
    #- Sensorprotokolle: AVR NET-IO, Ethersex, Voltmeter (z.B. McVoice M-980T TRUE REMS MULTIMETER)
    #- Webserver integrieren, um Werte anliefern oder die Software fernsteuern zu können
    #- Anzeige der Werte als laufend aktualisierte Kurve.
    #- Anzeige der geloggten Werte aus der Logdatei.
    #- Skalierungsfunktionen, Auto-Skalierung anhand der aufgetretenen Werte.
    #- XY-Anzeige (z.B. Temperatur über Licht), für Kennlinienschreiber o.ä.
    #- Kurven als Grafik speichern.
    #- Eigene Bezeichnungen für Ein- und Ausgänge definierbar machen
    #- Andere grafische Widgets: Digitalanzeige, Analoganzeige usw.
    #- Anwendungsbezogene Spezial-Widgets, z.B. Tür-Reedsensor => Türsymbol offen/geschlossen
    #- Widgets anzeigen oder weglassen, anders anordnen, Auswahl unterschiedlicher Widgets
    #- Fehlerbehandlung bei Verbindungsausfall
    #- Fehlerbehandlung bei Logfile-Problemen
    #- Umstellung der Netzwerkparameter auf eigene Wunschwerte
    #- Bedienung mehrerer Boards
    #- Weitere (alle) Funktionen der Pollin-Software nachbilden
    #- Umdefinieren der Portfunktionen (dann ist es nicht mehr der AVR NET-IO "out of the box" und benötigt eine andere Firmware)
    
    
    import time
    import telnetlib
    import Tkinter
    
    #=======================================================
    
    #AVR NET-I/O Default Parameters:
    #IP = 192.168.0.90
    #NETMASK = 255.255.255.0
    #GATEWAY = 192.168.0.254
    #TELNET PORT = 50290
    #Commands:
    # GETPORT x
    # GETADC x
    # SETPORT x.y
    # GETSTATUS
    # GETIP
    # SETIP x.x.x.x
    # GETMASK
    # SETMAST x.x.x.x
    # GETGW
    # SETGW x.x.x.x
    # INITLCD
    # WRITELCD x.y
    # CLEARLCD x
    # VERSION
    # RESET
    
    #Default network parameters
    telnethost = '192.168.0.90'
    telnetport = 50290
    
    outfilename = 'avrnetio.log'
    Standard_Interval = 100 #in 1/100 seconds
    
    #Set this to False if you want to reduce disk access
    #Set this to True if you watch the output visually with "tail -f" or if you want to save avery query immediately
    Logfile_open_close_for_each_entry = True
    
    #=======================================================
    
    # Connecting to device / initializing:
    
    print 'Connecting to AVR NET-IO with telnet at IP %s on port %d' % (telnethost, telnetport)
    
    #Connect on telnet port
    netio = telnetlib.Telnet(telnethost, telnetport)
    
    #send command and get results
    def sg(netio, cmd):
    	netio.write(cmd + '\n')
    	return netio.read_until('\n').strip('\r\n')
    
    #get version
    def version(netio): 
    	print 'Version info:'
    	print sg(netio,'version')
    	print netio.read_until('\n').strip('\r\n')
    	print netio.read_until('\n').strip('\r\n')
    
    print
    version(netio)
    
    #get ipparams - but they are known when you can connect with telnet.
    def ipparams(netio):
    	print 'IP parameters:'
    	print 'IP:     ', sg(netio,'getip')
    	print 'Netmask:', sg(netio,'getmask')
    	print 'Gateway:', sg(netio,'getgw')
    
    print
    ipparams(netio)
    
    #Get values of all ADCs and Status
    def adcs(netio):
    	for i in [1,2,3,4]:
    		print 'ADC' + str(i) + ': ' + sg(netio,'getadc ' + str(i)).rjust(4) + ' -',
    	print sg(netio,'getstatus')
    
    #Get value of specific ADC
    def adc(netio,i):
    	return int(sg(netio,'getadc ' + str(i)))
    
    print
    print 'Blinking outputs...'
    #Some blinking of outputs, for fun
    for i in range(1): # Set higher value for longer blinkery
    	sg(netio,'setport 1.1')
    	time.sleep(0.1)
    	sg(netio,'setport 1.0')
    	sg(netio,'setport 2.1')
    	time.sleep(0.1)
    	sg(netio,'setport 2.0')
    	sg(netio,'setport 3.1')
    	time.sleep(0.1)
    	sg(netio,'setport 3.0')
    	sg(netio,'setport 4.1')
    	time.sleep(0.1)
    	sg(netio,'setport 4.0')
    	time.sleep(0.3)
    
    print 'Done initializing.'
    print
    
    #netio.close()
    
    #=======================================================
    
    # For automatic logging:
    
    #Connect and get AD values and Status of inputs
    def getads(netio):
    	try:
    		netio = telnetlib.Telnet(telnethost, telnetport)
    		a1 = int(adc(netio,1))
    		a2 = int(adc(netio,2))
    		a3 = int(adc(netio,3))
    		a4 = int(adc(netio,4))
    		s = sg(netio,'getstatus')
    		flag = 'OK'
    	except:
    		a1, a2, a3, a4, s = 0, 0, 0, 0, 0
    		flag = 'Error'
    	netio.close()
    	return a1, a2, a3, a4, s, flag
    
    #=======================================================
    
    # GUI
    
    print 'Starting graphical user interface (GUI)'
    
    #Farben für digitale Buttons
    color_off_bg = 'green'
    color_off_fg = 'black'
    color_on_bg = 'yellow'
    color_on_fg = 'black'
    
    def Exit():
    	global Continue
    	print 'Exit requestet. Stopping program.'
    	Continue = False
    
    window = Tkinter.Tk()
    window['bg'] = 'blue'
    #window['command'] = Exit
    window.title('AVR NET-IO')
    
    #window.config(width = 200, height = 200)
    ADC = []
    Input = []
    Output = []
    
    #Exit/Logging/Refresh block
    f1 = Tkinter.Frame(window)
    f1.pack(fill = 'x', side = 'top')
    
    #ADC block
    f2 = Tkinter.Frame(window)
    f2.pack(side = 'top')
    
    #Input/Output block
    f5 = Tkinter.Frame(window, bg = 'blue', padx = 10, pady = 10)
    f5.pack(side = 'right')
    
    #Refresh slider
    refresh = Tkinter.Scale(f1, orient='horizontal', length=400, label = 'Refresh interval', cursor = 'hand2', command = window.update())
    refresh['from'] = 0
    refresh['to'] = 200
    refresh.set(Standard_Interval)
    refresh.pack(side = 'right')
    
    #Exit button
    x = Tkinter.Button(f1, text = 'Exit!', background = 'grey', cursor = 'hand1')
    x['command'] = Exit
    x.pack(side = 'left')
    
    #Log start button
    log = Tkinter.Button(f1, text = 'Start logging!', background = 'red', cursor = 'hand2')
    
    Logging = False
    outfile = None
    def logtoggle():
    	global Logging
    	global outfile
    	
    	#Switch logging flag
    	Logging = not Logging
    	
    	if Logging: #so we just turned it on
    		if not Logfile_open_close_for_each_entry: #(In that other case the file is opened and closed for each log entry)
    			#Open output file in current directory
    			outfile = open(outfilename, 'a')
    		print 'Logging started into file:', outfilename
    	else:
    		if not Logfile_open_close_for_each_entry: #(In that other case the file is opened and closed for each log entry
    			outfile.close()
    		print 'Logging stopped.'
    
    log['command'] = logtoggle
    log.pack(side = 'left')
    
    #Timestamp
    t = Tkinter.Label(f1, text = "Timestamp: ")
    t.pack(side = 'top')
    
    #Data
    d = Tkinter.Label(f1, text = "Data: ")
    d.pack(side = 'top')
    
    #Logfile
    l = Tkinter.Label(f1, text = "Logfile: " + outfilename)
    l.pack(side = 'top')
    
    
    f3 = Tkinter.Frame(window, bg = 'blue', padx = 10, pady = 10)
    f3.pack(side='left')
    f4 = Tkinter.Frame(window, bg = 'red')
    f4.pack(side='left')
    
    #Vier Regler-Widgets für die vier AD-Wandler definieren
    for i in range(4):
    	ADC.append(Tkinter.Scale(f2, orient='horizontal', length=1024, label='ADC ' + str(i + 1), foreground = 'blue', background = 'green'))
    	ADC[i]['from']=0
    	ADC[i]['to']=1023
    	ADC[i].pack()
    
    def toggle1(): sg(netio,'setport 1.' + ('1' if Output[0]['bg'] == color_off_bg else '0') ) #einschalten
    def toggle2(): sg(netio,'setport 2.' + ('1' if Output[1]['bg'] == color_off_bg else '0') ) #einschalten
    def toggle3(): sg(netio,'setport 3.' + ('1' if Output[2]['bg'] == color_off_bg else '0') ) #einschalten
    def toggle4(): sg(netio,'setport 4.' + ('1' if Output[3]['bg'] == color_off_bg else '0') ) #einschalten
    def toggle5(): sg(netio,'setport 5.' + ('1' if Output[4]['bg'] == color_off_bg else '0') ) #einschalten
    def toggle6(): sg(netio,'setport 6.' + ('1' if Output[5]['bg'] == color_off_bg else '0') ) #einschalten
    def toggle7(): sg(netio,'setport 7.' + ('1' if Output[6]['bg'] == color_off_bg else '0') ) #einschalten
    def toggle8(): sg(netio,'setport 8.' + ('1' if Output[7]['bg'] == color_off_bg else '0') ) #einschalten
    
    #Acht Buttons für die acht Digitalausgänge definieren
    for i in range(8):
    	Output.append(Tkinter.Button(f5, cursor = 'hand2'))
    	Output[i].pack(side = 'left')
    Output[0].config(text='Output 1', command = toggle1)
    Output[1].config(text='Output 2', command = toggle2)
    Output[2].config(text='Output 3', command = toggle3)
    Output[3].config(text='Output 4', command = toggle4)
    Output[4].config(text='Output 5', command = toggle5)
    Output[5].config(text='Output 6', command = toggle6)
    Output[6].config(text='Output 7', command = toggle7)
    Output[7].config(text='Output 8', command = toggle8)
    
    
    #Vier Kontrollkästchen zur Ausgabe der vier Digitaleingänge definieren
    for i in range(4):
    	Input.append(Tkinter.Checkbutton(f3))
    	Input[i].config(text='Input ' + str(i + 1))
    	Input[i].pack(side = 'left')
    
    print 'Displaying values... (abort with Ctrl+C)'
    
    Log_count = 0
    Continue = True
    while Continue:
    	timestamp = time.time()
    	
    	#Daten von Board holen
    	a1, a2, a3, a4, Status, flag = getads(netio)
    	
    	#Eingänge abfragen
    	Inputs = 'I'
    	for i in range(4):		
    		if sg(netio,'getport ' + str(4-i) ) == '1':
    			Input[i].select()
    			Inputs += '1'
    		else:
    			Input[i].deselect()
    			Inputs += '0'
    
    	#Timestamp und Daten als Text ausgeben
    	d['text'] = "Data: %4d - %4d - %4d - %4d - %s - %s - %s" % (a1, a2, a3, a4, Status, Inputs, flag)
    	t['text'] = "Timestamp: %.2f" % timestamp
    	
    	#Werte der AD-Wandler als Regler anzeigen
    	ADC[0].set(a1)
    	ADC[1].set(a2)
    	ADC[2].set(a3)
    	ADC[3].set(a4)
    	
    	#Status der Digitalausgänge abfragen und anzeigen
    	#Rückgabeformat: 'S01010011' (S = fest, dann die Bits der Abfrage)
    	for i in range(8):
    		if (Status[8-i] != '0'): #on
    			Output[i]['bg'] = color_on_bg
    			Output[i]['fg'] = color_on_fg
    		else: #off
    			Output[i]['bg'] = color_off_bg
    			Output[i]['fg'] = color_off_fg
    	
    	if not Logging:
    		log.configure(background = 'red', text = 'Start logging')
    	else: #logging is on
    		log.configure(background = 'green', text = 'Stop logging')
    		
    		#log values
    		if Logfile_open_close_for_each_entry: outfile = open(outfilename, 'a')
    		Log_count += 1
    		outfile.write(  str(time.time()) + '\t' + str(Log_count) + '\t' + str(a1) + '\t' + str(a2) + '\t' + str(a3) + '\t' + str(a4) + '\t' + Status + '\t' + Inputs + '\t' + flag + '\n' ) #And write them to logfile
    		if Logfile_open_close_for_each_entry: outfile.close()
    	
    	window.update()
    	wait =  refresh.get() / 100.0
    	refresh['label'] = 'Wait time between queries: %.2f s' % wait
    	time.sleep( wait )
    
    
    # Set your logging parameters here:
    
    #outfilename = 'avrnetio.log'
    #loginterval = 30 #seconds
    
    
    #Endless logging loop which prints values and writes them to a file.
    #i = 0	#Counter of logged values since start of script.
    #t0=time.time() #One of the time correction variables
    #while True: #Set a limit if you want
    	#i += 1
    	#print time.time(), '-', i, '-',  #Start log line with unix timestamp (with second fractions), and counter
    	#a1, a2, a3, a4, s, flag = getads(netio)	#Get input values from controller
    	#print a1, '-', a2, '-', a3, '-', a4, '-', s, '-', flag #Print them
    	#outfile.write(  str(time.time()) + '\t' + str(i) + '\t' + str(a1) + '\t' + str(a2) + '\t' + str(a3) + '\t' + str(a4) + '\t' + str(s) + '\t' + flag + '\n' ) #And write them to logfile
    	#t1=time.time() #These lines correct for execution time of loop in order to get equidistant intervalls.
    	#t2=time.time()
    	#time.sleep(loginterval - (t1-t0 - (t2-t1)) ) #Sleep for time corrected interval
    	#t0=time.time()
    
    
    #Properly close file, if loop is left while logging
    if outfile and not Logfile_open_close_for_each_entry:
    	outfile.close()
    
    netio.close()
    
    print 'Done. Goodbye!'
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

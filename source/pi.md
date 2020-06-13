---
title: pi
date: 2020-05-07
---
Example Python program pi.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import sys
* import subprocess

## Methods

* def print_wiki_options(file) :
* def print_wiki_article(file):
* def print_menu():
* def main():

## Code

Python example

    #!/usr/bin/env python
    
    import sys
    import subprocess
    
    def print_wiki_options(file) :
        subprocess.call("clear")
        with open(file, 'r') as f :
            for line in f:
                sys.stdout.write(line)
    
    def print_wiki_article(file):
        subprocess.call("clear")
        # This is how you open a file in Python, read it line by line, and print
        # it to STDOUT.
        #
        # Note that file name paths are relative.
        #   
        # 'cpu.txt'
        # 'nokia/cpu.txt'
        # '/home/ssimpson/nokia/cpu.txt'
        with open(file, 'r') as f:
               # Here we do a for loop, where we iterate over every line in the file.       
               for line in f:
               # We do NOT want to use ``print`` here, because print automatically 
               # puts a newline character at the end of each line.  This is a problem because
               # most lines in the ticket procedure files have a `\n` character at the end of
               # each line, which would result in two new lines.
               #
               # Thus, we use the ``sys.stdout.write`` function to print the line 
               # exactly how it appears in the file.
               sys.stdout.write(line)
        print ""
        raw_input("Press any key and hit enter ")
    
    def print_menu():
        # This is an example on how to do a multi-line string in Python. This is one
        # way to make it easier for editing menus/prompts for your command line
        # program.
        #
        # Note that you do NOT want to indent the lines after the first, as this
        # will mess up your spacing when you print it.
        menu = """###########################################################
                         non shity wiki
                          VERSION 1337
                      CREATOR: st3v3n s1mps0n
    ###########################################################
                            MAIN MENU
    1:Nokia.........................................5:GAiA
    2:Crossbeam.....................................6:Imperva
    3:SRX...........................................7:TPConsole
    4:Netscreen.....................................8:TPSensor
    .......................9:CitrixWAF:.......................
    ###########################################################
                      PLEASE CHOOSE A PLATFORM
    """
        
        print menu
        
    # This is our main function that runs our program.
    def main():
        while True:
            subprocess.call ("clear")
            print_menu()
            input=raw_input()
                subprocess.call ("clear")
            #
            #
            # Now you can create new wiki article files (i.e. 'nokia_cpu.txt') and
            # easily print them to STDOUT:
            #
            #   print_wiki_article('nokia_cpu.txt')
            #   print_wiki_article('nokia_foo.txt')
            #   etc
            #
            #
            # Nested if statements where the appropriate 
            # "artcle" and "options" are selected by the 
            # user via input
            #
            #
            #
            
            
            if input == "1":
            print_wiki_options('/root/Documents/python/Nokia/NokiaTickets')
            input=raw_input()
        
            if input =="1":
                 print_wiki_article('/root/Documents/python/Nokia/Nokia_CPU')
                elif input =="2":
                 print_wiki_article('/root/Documents/python/Nokia/Nokia_CPHA')
            elif input =="3":
                 print_wiki_article('/root/Documents/python/Nokia/Nokia_FWMax')
            elif input =="4":
                 print_wiki_article('/root/Documents/python/Nokia/Nokia_HWCheck')
            elif input =="5":
                 print_wiki_article('/root/Documents/python/Nokia/Nokia_IntErrors')
            elif input =="6":
                 print_wiki_article('/root/Documents/python/Nokia/Nokia_LogConn')
            elif input =="7":
                 print_wiki_article('/root/Documents/python/Nokia/Nokia_VRRP')  
    
            
            elif input == "2":
            print_wiki_options('/root/Documents/python/Crossbeam/CrossbeamTickets')
            input=raw_input()
            
              
            if   input =="1":
                 print_wiki_article('/root/Documents/python/Crossbeam/Crossbeam_CPD')
            elif input =="2":
                  print_wiki_article('/root/Documents/python/Crossbeam/Crossbeam_CPU')
            elif input =="3":
                  print_wiki_article('/root/Documents/python/Crossbeam/Crossbeam_Disk')
            elif input =="4":
                  print_wiki_article('/root/Documents/python/Crossbeam/Crossbeam_Mem')
    
            
            elif input == "3":
            print_wiki_options('/root/Documents/python/SRX/SRXTickets')
            input=raw_input()
    
            if   input =="1":
             print_wiki_article('/root/Documents/python/SRX/SRX_IntErrors')
            elif input =="2":
                print_wiki_article('/root/Documents/python/SRX/SRX_CPU')
            elif input =="3":
                print_wiki_article('/root/Documents/python/SRX/SRX_DiskUsage')
                elif input =="4":
                print_wiki_article('/root/Documents/python/SRX/SRX_MemUsage')
                elif input =="5":
                print_wiki_article('/root/Documents/python/SRX/SRX_ClusterStatus')
                elif input =="6":
                print_wiki_article('/root/Documents/python/SRX/SRX_CoreFile')
            
            elif input == "4":
            print_wiki_options('/root/Documents/python/Netscreen/NetscreenTickets')
            input=raw_input()
    
            if   input =="1":
                print_wiki_article('/root/Documents/python/Netscreen/Netscreen_CPU')
            elif input =="2":
                print_wiki_article('/root/Documents/python/Netscreen/Netscreen_IDPBlade')
            elif input =="3":
                print_wiki_article('/root/Documents/python/Netscreen/Netscreen_Chassis')
            elif input =="4":
                print_wiki_article('/root/Documents/python/Netscreen/Netscreen_Failover')
            elif input =="5":
                print_wiki_article('/root/Documents/python/Netscreen/Netscreen_FailoverChannels')
            elif input =="6":
                print_wiki_article('/root/Documents/python/Netscreen/Netscreen_MasterBackupStatus')
            
            elif input == "5":
             print_wiki_options('/root/Documents/python/GAiA/GAiATickets')
             input=raw_input()
    
             if  input =="1":
                print_wiki_article('/root/Documents/python/GAiA/GAiA_Temp')
             elif input =="2":
                print_wiki_article('/root/Documents/python/GAiA/GAiA_CPU')
             elif input =="3":
                print_wiki_article('/root/Documents/python/GAiA/GAiA_Chassis')
             elif input =="4":
                print_wiki_article('/root/Documents/python/GAiA/GAiA_Health')
             elif input =="5":
                print_wiki_article('/root/Documents/python/GAiA/GAiA_Route')
            
            elif input == "6":
             print_wiki_options('/root/Documents/python/Imperva/ImpervaTickets')
             input=raw_input()
    
             if  input =="1":
                print_wiki_article('/root/Documents/python/Imperva/Imperva_Disk')
             elif input =="2":
                print_wiki_article('/root/Documents/python/Imperva/Imperva_IntErrors')
             elif input =="3":
                print_wiki_article('/root/Documents/python/Imperva/Imperva_RaidStatus')
            
            elif input == "7":
             print_wiki_options('/root/Documents/python/TPConsole/TPConsoleTickets')
             input=raw_input()
    
             if  input =="1":
                print_wiki_article('/root/Documents/python/TPConsole/TPConsole_IntErrors')
                 elif input =="2":
                print_wiki_article('/root/Documents/python/TPConsole/TPConsole_MonitoringStatus')
                 elif input =="3":
                print_wiki_article('/root/Documents/python/TPConsole/TPConsole_PowerSupply')
             elif input =="4":
                print_wiki_article('/root/Documents/python/TPConsole/TPConsole_SensorDiskSpace')
             elif input =="5":
                print_wiki_article('/root/Documents/python/TPConsole/TPConsole_SMSHA')
                
            elif input == "8":
             print_wiki_options('/root/Documents/python/TPSensor/TPSensorTickets')
             input=raw_input()
    
             if  input =="1":
                print_wiki_article('/root/Documents/python/TPSensor/TPSensor_CPU')
             elif input =="2":
                print_wiki_article('/root/Documents/python/TPSensor/TPSensor_HAState')
             elif input =="3":
                print_wiki_article('/root/Documents/python/TPSensor/TPSensor_IntErrors')
                 elif input =="4":
                print_wiki_article('/root/Documents/python/TPSensor/TPSensor_MemoryUtil')
             elif input =="5":
                print_wiki_article('/root/Documents/python/TPSensor/TPSensor_PowerSupply')
                
            elif input == "9":
             print_wiki_options('/root/Documents/python/CitrixWAF/CitrixWAFTickets')
             input=raw_input()
    
             if input =="1":
                print_wiki_article('/root/Documents/python/CitrixWAF/CitrixWAF_MemoryUtil')
             elif input =="2":
                print_wiki_article('/root/Documents/python/CitrixWAF/CitrixWAF_CPU')
             elif input =="3":
                print_wiki_article('/root/Documents/python/CitrixWAF/CitrixWAF_PingDown')
                   
            elif input =="0":           
                     break  
    
    # This is the proper way to start a Python program.
    if __name__ == '__main__':
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

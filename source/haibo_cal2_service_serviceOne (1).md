---
title: haibo_cal2_service_serviceOne (1)
date: 2020-05-07
---
Example Python program haibo_cal2_service_serviceOne (1).py

## Modules

* import numpy as np

## Methods

* def executeCal1(self, filename, targetCatalog):

## Code

Python example

    # -*-coding:utf-8 -*-
    import numpy as np
    
    
    def executeCal1(self, filename, targetCatalog):
        number_max = 399
        mark_area = 0.0314
    
        read = open(filename)
    
        F = open(targetCatalog + '\\report.txt', 'w')
        f = open(targetCatalog + '\\report_detail.txt', 'w')
    
        line = read.readline()
        while line != '*\n':
            if line != '\n':
                title = line
                line = read.readline()
                line = read.readline()
    
                voltage = np.zeros(number_max)
                current = np.zeros(number_max)
                efficiency = np.zeros(number_max)
                index = 0
                while line != '\n':
                    Line_list = line.split()
                    if float(Line_list[2]) < 0:
                        voltage[index] = float(Line_list[0])
                        current[index] = float(Line_list[2])
                        index = index + 1
                    line = read.readline()
    
                current = current * -1000 / mark_area
                efficiency = current * voltage
    
                Efficiency = np.max(efficiency)
                Voltage = np.max(voltage)
                Current = np.max(current)
                FF = Efficiency / Voltage / Current
    
                F.write(title)
                F.write(".................................................................................")
                F.write('\n')
                # 写入效率
                F.write("效率为")
    
                F.write(str(Efficiency))
                F.write('\n')
                # 写入电压
                F.write("电压为")
    
                F.write(str(Voltage))
                F.write('\n')
                # 写入电流
                F.write("电流为")
    
                F.write(str(Current))
                F.write('\n')
                # 写入填充因子
                F.write("填充因子为")
                F.write("\000")
                F.write(str(FF))
                F.write('\n')
                F.write('\n')
    
                f.write(title)
                f.write(".................................................................................")
                f.write('\n')
                # 写入效率
                f.write("效率为")
                f.write(str(Efficiency))
                f.write('\n')
                # 写入电压
                f.write("电压为")
                f.write(str(Voltage))
                f.write('\n')
                # 写入电流
                f.write("电流为")
                f.write(str(Current))
                f.write('\n')
                # 写入填充因子
                f.write("填充因子为")
                f.write(str(FF))
                f.write('\n')
    
                f.write("Voltage\000")
                f.write("Current\n")
    
                for i in range(number_max):
                    if voltage[i] != 0 or current[i] != 0:
                        line_output_voltage = str(voltage[i]) + "\000"
                        line_output_current = str(current[i]) + "\n"
                        f.write(line_output_voltage)
                        f.write(line_output_current)
                f.write('\n')
            else:
                line = read.readline()
        F.close()
        f.close()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

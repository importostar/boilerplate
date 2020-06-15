---
title: statistics (1)
date: 2020-05-07
---
Example Python program statistics (1).py

## Modules

* import tkinter
* import math

## Methods

* def initialize():
* def go_to_stats():
* def get_data():
* def get_sum(list):
* def get_mean(list):
* def get_stddev(list):
* def sort_ascend(list):
* def get_min(list):
* def get_max(list):
* def get_medium(list):

## Code

Python tkinter example

    import tkinter
    
    import math
    
    
    data_values = []
    data_values_2 = []
    data_values_3 = []
    sum = 0
    sum2 = 0
    sum3 = 0
    mean = 0
    mean2 = 0
    mean3 = 0
    stddev = 0
    stddev2 = 0
    stddev3 = 0
    data_path = "C:/Users/msl/PycharmProjects/untitled1/data.csv"
    now_char = ""
    now_str = ""
    now_line = 0
    now_char_num = 0
    
    
    def initialize():
        home = tkinter.Tk()
    
        instructions = tkinter.Label(home, text="enter the file path and name for the data below, then click ok")
        instructions.pack(side="top")
    
        data_list = tkinter.Entry(home, bd=5, textvariable=data_path)
        data_list.pack(side="top")
    
        go = tkinter.Button(home, text="ok", command=go_to_stats)
        go.pack(side="top")
    
        home.mainloop()
    
    
    def go_to_stats():
        get_data()
    
        sum = get_sum(data_values)
        mean = get_mean(data_values)
        stddev = get_stddev(data_values)
        min = get_min(data_values)
        med = get_medium(data_values)
        max = get_max(data_values)
        sum2 = get_sum(data_values_2)
        mean2 = get_mean(data_values_2)
        stddev2 = get_stddev(data_values_2)
        min2 = get_min(data_values_2)
        med2 = get_medium(data_values_2)
        max2 = get_max(data_values_2)
        sum3 = get_sum(data_values_3)
        mean3 = get_mean(data_values_3)
        stddev3 = get_stddev(data_values_3)
        min3 = get_min(data_values_3)
        med3 = get_medium(data_values_3)
        max3 = get_max(data_values_3)
    
        sum_str = "sum: " + str(sum)
        mean_str = "mean: " + str(mean)
        stddev_str = "standard deviation: " + str(stddev)
        min_str = "min: " + str(min)
        max_str = "max: " + str(max)
        sum_str2 = "sum: " + str(sum2)
        mean_str2 = "mean: " + str(mean2)
        stddev_str2 = "standard deviation: " + str(stddev2)
        min_str2 = "min:" + str(min2)
        max_str2 = "max: " + str(max2)
        sum_str3 = "sum: " + str(sum3)
        mean_str3 = "mean: " + str(mean3)
        stddev_str3 = "standard deviation: " + str(stddev3)
        min_str3 = "min: " + str(min3)
        max_str3 = "max: " + str(max3)
    
        stats_window = tkinter.Tk()
        sum_box = tkinter.Label(stats_window, text=sum_str)
        sum_box.grid(row=1, column=1)
        mean_box = tkinter.Label(stats_window, text=mean_str)
        mean_box.grid(row=2, column=1)
        stddev_box = tkinter.Label(stats_window, text=stddev_str)
        stddev_box.grid(row=3, column=1)
        min_box = tkinter.Label(stats_window, text=min_str)
        min_box.grid(row=4, column=1)
        max_box = tkinter.Label(stats_window, text=max_str)
        max_box.grid(row=6, column=1)
        sum_box2 = tkinter.Label(stats_window, text=sum_str2)
        sum_box2.grid(row=1, column=2)
        mean_box2 = tkinter.Label(stats_window, text=mean_str2)
        mean_box2.grid(row=2, column=2)
        stddev_box2 = tkinter.Label(stats_window, text=stddev_str2)
        stddev_box2.grid(row=3, column=2)
        min_box2 = tkinter.Label(stats_window, text=min_str2)
        min_box2.grid(row=4, column=2)
        max_box2 = tkinter.Label(stats_window, text=max_str2)
        max_box2.grid(row=6, column=2)
        sum_box3 = tkinter.Label(stats_window, text=sum_str3)
        sum_box3.grid(row=1, column=3)
        mean_box3 = tkinter.Label(stats_window, text=mean_str3)
        mean_box3.grid(row=2, column=3)
        stddev_box3 = tkinter.Label(stats_window, text=stddev_str3)
        stddev_box3.grid(row=3, column=3)
        min_box3 = tkinter.Label(stats_window, text=min_str3)
        min_box3.grid(row=4, column=3)
        max_box3 = tkinter.Label(stats_window, text=max_str3)
        max_box3.grid(row=6, column=3)
    
    
    def get_data():
    
        with open(data_path, 'r', newline="") as data_set:
            now_str = ""
            now_char_num = 0
            now_char = ""
            list = 1
    
            while now_char_num < 10 ** 6:
                now_char = data_set.read(1)
                now_char_num += 1
                if now_char != ("0" or "1" or "2" or "3" or "4" or "5" or "6" or "7" or "8" or "9" or "-" or "."):
                    if now_char == ",":
                        if list == 1:
                            data_values.append(float(now_str))
                        elif list == 2:
                            data_values_2.append(float(now_str))
                        elif list == 3:
                            data_values_3.append(float(now_str))
                        now_str = ""
                        list += 1
                    elif now_char == "\n":
                        data_values_3.append(float(now_str))
                        list = 1
                        now_str = ""
                    else:
                        now_str += now_char
                else:
                    now_str += now_char
    
    
    def get_sum(list):
        fsum = 0
        for number in list:
            fsum += number
        return fsum
    
    
    def get_mean(list):
        fmean = 0
        fsum = get_sum(list)
        if len(list) > 0:
            fmean = fsum / len(list)
        return fmean
    
    
    def get_stddev(list):
        stddv = 0
        fmean = get_mean(list)
        for n in list:
            stddv += (n - fmean) ** 2
        if len(list) > 0:
            stddv = math.sqrt(stddv / len(list))
        return stddv
    
    
    def sort_ascend(list):
        listAscend = list
        for i in range(0, len(list) - 2):
            for j in range(len(list) - 1, i+1):
                if listAscend[i] > listAscend[j]:
                    temp = listAscend[i]
                    listAscend[i] = listAscend[j]
                    listAscend[j] = temp
        return listAscend
    
    
    def get_min(list):
        i = 1
        fmin = 0
        for n in list:
            if i == 1:
                fmin = n
                i += 1
            if fmin > n:
                fmin = n
        return fmin
    
    
    def get_max(list):
        i = 1
        fmax = 0
        for n in list:
            if i == 1:
                fmax = n
                i += 1
            if fmax < n:
                fmax = n
        return fmax
    
    
    def get_medium(list):
        flist = sort_ascend(list)
        n = (len(flist) - 1) / 2.0
        #o = len(flist) % 2
        if n % 1 == .5:
            o = int(math.floor(n))
            fmed = (flist[o] + flist[0 + 1])/2
        else:
            fmed = flist[n]
        return fmed
    
    
    
    
    initialize()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: statistics
date: 2020-05-07
---
Example Python program statistics.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import collections
* import math
* import sys

## Methods

* def main():
* def read_data(filename, numbers, frequencies):
* def calculate_statistics(numbers, frequencies):
* def calculate_mode(frequencies, maximum_modes):
* def calculate_median(numbers):
* def calculate_std_dev(numbers, mean):
* def print_results(count, statistics):

## Code

Python example

    import collections
    import math
    import sys
    
    
    Statistics = collections.namedtuple("Statistics",
                                        "mean mode median std_dev")
    
    
    def main():
        if len(sys.argv) == 1 or sys.argv[1] in {"-h", "--help"}:
            print("usage: {0} file1 [file2 [... fileN]]".format(
                  sys.argv[0]))
            sys.exit()
    
        numbers = []
        frequencies = collections.defaultdict(int)
        for filename in sys.argv[1:]:
            read_data(filename, numbers, frequencies)
        if numbers:
            statistics = calculate_statistics(numbers, frequencies)
            print_results(len(numbers), statistics)
        else:
            print("no numbers found")
    
    
    def read_data(filename, numbers, frequencies):
        with open(filename, encoding="ascii") as file:
            for lino, line in enumerate(file, start=1):
                for x in line.split():
                    try:
                        number = float(x)
                        numbers.append(number)
                        frequencies[number] += 1
                    except ValueError as err:
                        print("{filename}:{lino}: skipping {x}: {err}".format(
                            **locals()))
    
    
    def calculate_statistics(numbers, frequencies):
        mean = sum(numbers) / len(numbers)
        mode = calculate_mode(frequencies, 3)
        median = calculate_median(numbers)
        std_dev = calculate_std_dev(numbers, mean)
        return Statistics(mean, mode, median, std_dev)
    
    
    def calculate_mode(frequencies, maximum_modes):
        highest_frequency = max(frequencies.values())
        mode = [number for number, frequency in frequencies.items()
                if frequency == highest_frequency]
        if not (1 <= len(mode) <= maximum_modes):
            mode = None
        else:
            mode.sort()
        return mode
    
    
    def calculate_median(numbers):
        numbers = sorted(numbers)
        middle = len(numbers) // 2
        median = numbers[middle]
        if len(numbers) % 2 == 0:
            median = (median + numbers[middle - 1]) / 2
        return median
    
    
    def calculate_std_dev(numbers, mean):
        total = 0
        for number in numbers:
            total += ((number - mean) ** 2)
        variance = total / (len(numbers) - 1)
        return math.sqrt(variance)
    
    
    def print_results(count, statistics):
        real = "9.2f"
    
        if statistics.mode is None:
            modeline = ""
        elif len(statistics.mode) == 1:
            modeline = "mode      = {0:{fmt}}\n".format(
                    statistics.mode[0], fmt=real)
        else:
            modeline = ("mode      = [" +
                        ", ".join(["{0:.2f}".format(m)
                        for m in statistics.mode]) + "]\n")
    
        print("""\
    count     = {0:6}
    mean      = {mean:{fmt}}
    median    = {median:{fmt}}
    {1}\
    std. dev. = {std_dev:{fmt}}""".format(
        count, modeline, fmt=real, **statistics._asdict()))
    
    
    main()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
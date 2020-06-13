---
title: bmi
date: 2020-05-07
---
Example Python program bmi.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Classes

* class Patient:

## Methods

* def __init__(self, name="UNKNOWN", gender="UNKNOWN", dob="UNKNOWN", ppsn="TESTING", weight=0.0, height=0.0):
* def calculate_bmi(self):
* def bmi_analysis(self):
* def generate_report(self):

## Code

Python example

    #!/usr/bin/python3
    
    """BMI calculator"""
    
    
    class Patient:
        """Creating patient class to model patient details for BMI calculation."""
    
        def __init__(self, name="UNKNOWN", gender="UNKNOWN", dob="UNKNOWN", ppsn="TESTING", weight=0.0, height=0.0):
            """Setting class attributes."""
            self.name = name
            self.gender = gender
            self.dob = dob
            self.ppsn = ppsn
            self.weight = weight
            self.height = height
    
        def calculate_bmi(self):
            """creating method to calculate body mass index, returns float
            BMI= weight(kg) / ( height(m)*height(m) )
    
            Example:
            >>> Patient(weight=75, height=1.7).calculate_bmi()
            25.95155709342561
            """
    
            return float(self.weight / (self.height * self.height))
    
        def bmi_analysis(self):
            """Analyse the patient's BMI:
            < 16 underweight, < 25 healthy, < 30 overweight, 30+ obese
    
            >>> Patient(height=1.83, weight=89).bmi_analysis()
            'overweight'
    
            """
            bmi = self.calculate_bmi()
            if bmi < 16:
                analysis = "underweight"
            elif bmi < 25:
                analysis = "healthy"
            elif bmi < 30:
                analysis = "overweight"
            else:
                analysis = "obese"
            return analysis
    
        def generate_report(self):
            """"Creating method to generate report to file containing patient details and BMI results."""
            report_file = open(self.ppsn, "w")
            print("PATIENT REPORT", file=report_file)
            print("-" * 30, "\n", file=report_file)
            print("Patient name:\t", self.name, file=report_file)
            print("Patient gender:\t", self.gender, file=report_file)
            print("Patient dob: \t", self.dob, file=report_file)
            print("Patient PPSN:\t", self.ppsn, file=report_file)
            print("Patient weight:\t", self.weight, "kg", file=report_file)
            print("Patient height:\t", self.height, "m", file=report_file)
            print("Patient BMI: \t", round(self.calculate_bmi(), 1), file=report_file)
            print("BMI Analysis: \t", self.bmi_analysis(), file=report_file)
            report_file.close()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

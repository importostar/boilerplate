---
title: 2014_survey_analysis
date: 2020-05-07
---
Example Python program 2014_survey_analysis.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import time
* import argparse
* import csv
* import matplotlib.pyplot

## Code

Python example

    import time
    import argparse
    import csv
    import matplotlib.pyplot
    
    parser = argparse.ArgumentParser()
    parser.add_argument("filepath", help="The filepath to the copy of the survey.")
    arguments = parser.parse_args()
    infile = open(arguments.filepath, encoding="latin-1")
    survey = infile.read()
    (questions, responses) = (survey.split("\n")[0], survey.split("\n")[1:])
    reader = csv.DictReader(responses, fieldnames=questions.split(","))
    response_rates = dict.fromkeys(questions.split(","), 0)
    questions_answered = []
    for response in reader:
        response_editable = response.copy()
        for field in response:
            if response[field] and response[field].strip():
                response_rates[field] += 1
            else:
                response_editable.pop(field)
        questions_answered.append(len(response_editable))
    survey_length = len(questions.split(","))
    print("Number of survey respondents:", len(responses))
    print("Number of questions:", survey_length)
    print("Average number of questions answered:",
          sum(questions_answered) / len(questions_answered))
    in_or_above_20th = 0
    for respondent in questions_answered:
        if respondent >= (survey_length / 10) * 2:
            in_or_above_20th += 1
    print("Number of survey respondents who answered 20% or more of the questions:",
          in_or_above_20th)
    ninety_percent = round(survey_length - (survey_length / 10))
    in_or_above_90th = 0
    for respondent in questions_answered:
        if respondent >= ninety_percent:
            in_or_above_90th += 1
    print("Number of survey respondents who answered 90% or more of the questions:",
          in_or_above_90th)
    response_rates_sortable = []
    for field in response_rates:
        response_rates_sortable.append((response_rates[field], field))
    response_rates_sortable.sort()
    response_rates_sortable.reverse()
    for field in response_rates_sortable:
        print(field[1] + ":", str(field[0]) + " out of " +
              str(len(questions_answered)))
    print("----")
    for field in response_rates_sortable:
        print(field[1] + ":" + "(" + str(field[0]) + ")",
              "=" * round(field[0] / 100))
    x = list(range(len(questions.split(","))))
    y = []
    for question in questions.split(","):
        y.append(response_rates[question])
    assert len(x) == len(y)
    matplotlib.pyplot.xlabel("Position of question on survey".title())
    matplotlib.pyplot.ylabel("Number of responses to question".title())
    matplotlib.pyplot.scatter(x,y)
    matplotlib.pyplot.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

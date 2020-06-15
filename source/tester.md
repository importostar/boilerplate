---
title: tester
date: 2020-05-07
---
Example Python program tester.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os
* import sys
* import pickle
* import random
* import tkinter
* import tkinter.filedialog

## Classes

* class bg:
* class Answer:
* class Question:
* class Tester:

## Methods

* def __init__(self, line):
* def __str__(self):
* def __init__(self, text):
* def addAnswer(self, answer):
* def test(self, answerStr):
* def getCorrectAnswers(self):
* def __str__(self):
* def __init__(self, fileName):
* def load(self):
* def shuffle(self):
* def run(self):
* def getStats(self):
* def save(self):
* def makeTester():

## Code

Python tkinter example

    #!/usr/bin/env python3
    
    import os
    import sys
    import pickle
    import random
    
    
    class bg:
        HEADER = '\033[95m'
        OKBLUE = '\033[94m'
        OKGREEN = '\033[92m'
        WARNING = '\033[93m'
        FAIL = '\033[91m'
        ENDC = '\033[0m'
        BOLD = '\033[1m'
        UNDERLINE = '\033[4m'
    
    
    class Answer:
    
        def __init__(self, line):
            self.text = line[1:].strip()
            self.correct = line.startswith('+')
    
        def __str__(self):
            return self.text
    
    
    class Question:
    
        def __init__(self, text):
            self.text = text
            self.answers = []
    
        def addAnswer(self, answer):
            self.answers.append(answer)
            random.shuffle(self.answers)
    
        def test(self, answerStr):
            for i, answer in enumerate(self.answers):
                if answer.correct and str(i + 1) not in answerStr:
                    return False
                elif not answer.correct and str(i + 1) in answerStr:
                    return False
    
            return True
    
        def getCorrectAnswers(self):
            str = ''
    
            str += bg.OKGREEN + 'Spravne odpovedi:\n' + bg.ENDC
            for i, answer in enumerate(self.answers):
                if answer.correct:
                    str += '{}{}){} {}\n'.format(bg.OKGREEN, i + 1, bg.ENDC, answer)
    
            str += bg.FAIL + 'Chybne odpovedi:\n' + bg.ENDC
            for i, answer in enumerate(self.answers):
                if not answer.correct:
                    str += '{}{}){} {}\n'.format(bg.FAIL, i + 1, bg.ENDC, answer)
    
            return str
    
        def __str__(self):
            return self.text
    
    
    class Tester:
    
        def __init__(self, fileName):
            self.fileName = fileName
            self.questions = []
            self.wrongQuestions = []
            self.cntCorrect = 0
            self.cntIncorrect = 0
    
            self.load()
            self.shuffle()
    
        def load(self):
            with open(self.fileName, encoding='utf8') as file:
                question = None
    
                for line in file:
                    line = line.strip()
    
                    if line == '':
                        pass
                    elif line.startswith('+') or line.startswith('-'):
                        question.addAnswer(Answer(line))
                    else:
                        question = Question(line)
                        self.questions.append(question)
    
        def shuffle(self):
            random.shuffle(self.questions)
    
        def run(self):
    
            cntQuestions = 0
    
            for question in self.questions:
    
                if cntQuestions < self.cntCorrect + self.cntIncorrect:
                    cntQuestions += 1
                    continue
    
                self.save()
    
                print('{}/{} :: {}'.format(self.cntCorrect + self.cntIncorrect, len(self.questions), question))
    
                for i, answer in enumerate(question.answers):
                    print('{}) {}'.format(i + 1, answer))
    
                answerStr = input('Zadejte odpoved: ')
                cntQuestions += 1
    
                if question.test(answerStr):
                    self.cntCorrect += 1
                    print()
                    print(bg.OKGREEN + 'Spravne' + bg.ENDC + ' - ' + self.getStats())
                    print()
                else:
                    self.cntIncorrect += 1
                    self.wrongQuestions.append(question)
                    print()
                    print(bg.FAIL + 'Spatne' + bg.ENDC + ' - ' + self.getStats())
                    print()
                    print(question.getCorrectAnswers())
    
            if len(self.wrongQuestions) > 0:
                ans = input('Nektere otazky jste zodpovedeli nespravne. Chcete si je zopakovat? a/n: ')
                if ans == 'a':
                    self.questions = self.wrongQuestions
                    self.wrongQuestions = []
                    self.cntCorrect = 0
                    self.cntIncorrect = 0
                    self.run()
    
            try:
                os.remove('__tester.pickle')
            except FileNotFoundError:
                pass
    
        def getStats(self):
            total = self.cntCorrect + self.cntIncorrect
            percentage = int((self.cntCorrect / total) * 100)
    
            return '{} ✔, {} ✗ - {}%\n'.format(self.cntCorrect, self.cntIncorrect, percentage)
    
        def save(self):
            with open('__tester.pickle', 'wb') as file:
                pickle.dump(self, file)
    
    
    def makeTester():
        fileName = None
    
        if len(sys.argv) > 1:
            fileName = sys.argv[1]
        else:
            try:
                import tkinter
                import tkinter.filedialog
    
                root = tkinter.Tk()
                root.withdraw()
                fileName = tkinter.filedialog.askopenfilename()
                root.destroy()
            except ImportError:
                pass
    
    
        if fileName == None or fileName == '' or fileName == ():
            print('Zadejte spravne soubor s otazkami')
            sys.exit(1)
    
        if os.path.isfile('__tester.pickle'):
            ans = input('Chcete pokracovat tam, kde jste naposledy skoncili? a/n: ')
    
            if ans == 'a':
                with open('__tester.pickle', 'rb') as file:
                    return pickle.load(file)
            else:
                return Tester(fileName)
        else:
            return Tester(fileName)
    
    
    if __name__ == '__main__':
        try:
            tester = makeTester()
            tester.run()
        except EOFError:
            pass
        except KeyboardInterrupt:
            pass
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

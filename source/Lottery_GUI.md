---
title: Lottery_GUI
date: 2020-05-07
---
Example Python program Lottery_GUI.py

## Modules

* import random
* import Tkinter
* import tkMessageBox

## Methods

* def main():
* def lottery_generate ():

## Code

Python tkinter example

    # Lottery number generator with GUI  by raidelmundo
    
    import random
    import Tkinter
    import tkMessageBox
    
    
    def main():
        Lottery_num = []
        how_many_numbers = 6
        number_max = 45
    
        how_many_numbers_int = int(how_many_numbers)
    
        window = Tkinter.Tk()
        window.minsize(width=900, height=400)
    
        hello_label = Tkinter.Label(window, text="Hi!\nThis is a Lottery number generator!")
        highest_num_label = Tkinter.Label(window, text="What is the highest number in your lottery?")
    
        hello_label.pack()
        highest_num_label.pack()
        number_max = Tkinter.Entry(window)
        number_max.pack()
    
        how_many_numbers_label = Tkinter.Label(window, text="How many random numbers do you want to generate? ")
        how_many_numbers = Tkinter.Entry(window)
        how_many_numbers_label.pack()
        how_many_numbers.pack()
    
    
        def lottery_generate ():
            how_many_numbers_int = int(how_many_numbers.get())
    
            while len(Lottery_num) <= how_many_numbers_int-1:
                if len(Lottery_num) == 0:
                    first_digit = random.randint(1, int(number_max.get()))
                    Lottery_num.append(first_digit)
                    tkMessageBox.showinfo("Your first number is: ", str(Lottery_num[0]))
                    print"First number is %d" %(first_digit)
                else:
                    following_digits = random.randint(1, int(number_max.get()))
                    if following_digits in Lottery_num:
                        continue
                    else:
                        Lottery_num.append(following_digits)
                        tkMessageBox.showinfo("The following number is: ", str(following_digits))
                        print"The following number is %d" %(following_digits)
    
            tkMessageBox.showinfo("Your generated and sorted numbers are: ", sorted(Lottery_num))
    
    
        # submit button
        submit = Tkinter.Button(window, text="Be Lucky! :)", command=lottery_generate)
        submit.pack()
        window.mainloop()
    
    
    if __name__ == "__main__":
        main()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

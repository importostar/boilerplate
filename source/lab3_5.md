---
title: lab3_5
date: 2020-05-07
---
Example Python program lab3_5.py

## Modules

* import InputBox
* import MessageBox

## Code

Python example

    import InputBox
    import MessageBox
    
    InputBox.ShowDialog("enter the first number:")
    n1 = InputBox.GetInput()
    n1 = float(n1)
    InputBox.ShowDialog("enter the second number:")
    n2 = InputBox.GetInput()
    n2 = float(n2)
    
    res = "Result:"
    Nsum = "sum:", str(n1 + n2)
    dif = "difference:", str(n1 - n2)
    pro ="product:", str(n1 * n2)
    quo = "quotient:", str(n1 / n2)
    remain = "remainder:", str(n1 % n2)
    intdiv = "integer division:", str(n1 // n2)
    ex = "exponent:", str(n1 ** n2)
    
    x1 = n1
    y1 = n2
    x1 += 1
    y1 -= 1
    
    inc1 = "increment by 1:", str(x1)
    dec1 = "decrement by 1:", str(y1)
    com1 = "(n1 >= n2:", n1 >= n2
    com2 = "(n1 == n2:", n1 == n2
    
    bitand = "bitwise and:", str(int(n1) & int(n2))
    bitor = "bitwise or:", str(int(n1) | int(n2))
    
    MessageBox.Show(str(res) + "\n" + str(Nsum) + "\n" + str(dif) + "\n" + str(pro) + "\n" + str(quo) + "\n" +
                    str(remain) + "\n" + str(intdiv) + "\n" + str(ex) + "\n" +
                    str(inc1) + "\n" + str(dec1) + "\n" + str(com1) + "\n" + str(com2) + "\n" + str(bitand) + "\n"
                    + str(bitor))
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

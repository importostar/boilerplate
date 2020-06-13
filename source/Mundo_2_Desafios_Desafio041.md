---
title: Mundo_2_Desafios_Desafio041
date: 2020-05-07
---
Example Python program Mundo_2_Desafios_Desafio041.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Code

Python example

    print('\nA confederação nacional de natação precisa de um programa que leia o ano de nascimento de um atleta e mostre sua\ncategoria, de acordo com a sua idade:'
          '\n-Até 9 anos: MIRIM'
          '\n-Até 14 anos: INFANTIL'
          '\n-Até 19 anos: JUNIOR'
          '\n-Até 20 anos: SÊNIOR'
          '\n-Acima: MASTER\n')
    
    idade = int(input('Informe a sua idade: '))
    
    if idade <= 9:
        print('A sua liga é a mirim.')
    elif idade > 9 and idade <= 14:
        print('A sua liga é a infantil.')
    elif idade > 14 and idade <=19:
        print('A sua liga é a junior.')
    elif idade > 19:
        print('A sua liga é a master.')
    elif idade <= 0 or idade >= 120:
        print('Não é possível competir com essa idade.')
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

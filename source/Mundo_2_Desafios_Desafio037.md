---
title: Mundo_2_Desafios_Desafio037
date: 2020-05-07
---
Example Python program Mundo_2_Desafios_Desafio037.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Code

Python example

    print('\nEscreva um programa que leia um número inteiro qualquer e peça para o usário escolher'
    'A base de conversão:'
    '\n1 -  para binário'
    '\n2 = para octal'
    '\n3 - para hexadecimal')
    
    num = int(input('Informe um número: '))
    esc = int(input('Digite 1 para binario, 2 para octal ou 3 para hexadecimal: '))
    
    if esc == 1:
        print('O número {} em binário fica: {}'.format(num, bin(num)))
    
    elif esc == 2:
        print('O número {} em octal fica: {}'.format(num, oct(num)))
    
    elif esc == 3:
        print('O número {} em hexadecimal fica: {}'.format(num, hex(num)))
    
    else:
        print('Você não escolheu nenhuma das opções.')

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

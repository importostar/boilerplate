---
title: Mundo_2_Desafios_Desafio042
date: 2020-05-07
---
Example Python program Mundo_2_Desafios_Desafio042.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Code

Python example

    print('\nRefaça o DESAFIO 035 dos triangulos, acrescentando o recurso de mostrar que tipo de triangulo será formado: '
          '\n- Equilátero:  todos os lados iguais'
          '\n- Isósceles: dois lados iguais'
          '\n- Escaleno: todos os lados diferentes')
    
    La = float(input('Informe o comprimento da primeira reta: '))
    Lb = float(input('agora da segunda reta: '))
    Lc = float(input('agora da terceira reta: '))
    
    if (Lb - Lc)< La <(Lb + Lc) and (La - Lc)< Lb <(La + Lc) and (La - Lb)< Lc <(La + Lb):
        if (La*Lb == Lb*Lc == La*Lc) == True:
            print('É possível formar um triangulo e ele será um triangulo Equilatero')
        elif (La*Lb==La*Lc) == True:
            print('É possivel formar um triangulo e ele será um triangulo Isosceles')
        elif (La*Lb != Lb*Lc != La*Lc) == True:
            print('É possível formar um triangulo e ele será um triangulo Escaleno')
    else:
        print('Não é possível formar um triangulo com essas medidas')

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: Mundo_2_Desafios_Desafio043
date: 2020-05-07
---
Example Python program Mundo_2_Desafios_Desafio043.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from math import pow

## Code

Python example

    print('\nDesenvolva uma lógica que leia o peso e a altura de uma pessoa, calcule seu IMC e mostre seu status, de acordo com\na tabela abaixo:'
          '\n-Abaixo de 18.5: Abaixo do peso'
          '\n-Entre 18.5 e 25: Peso ideal'
          '\n-25 até 30: Sobrepeso'
          '\n-30 até 40: Obesidade'
          '\n-Acima de 40: Obesidade mórbida\n')
    
    from math import pow
    
    altura = float(input('Informe a sua altura: '))
    peso = float(input('Informe o seu peso: '))
    
    imc = peso / (altura*altura)
    print('{:.1f}'.format(imc))
    
    if imc < 18.5:
        print('Você está abaixo do peso.')
    elif imc >= 18.5 and imc < 25:
        print('Você está no peso ideal.')
    elif imc >= 25 and imc < 30:
        print('Você está com sobrepeso')
    elif imc >= 30  and imc <40:
        print('Você está com obesidade')
    elif imc > 40:
        print('Você está com obesidade mórbida')

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

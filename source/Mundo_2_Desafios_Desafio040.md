---
title: Mundo_2_Desafios_Desafio040
date: 2020-05-07
---
Example Python program Mundo_2_Desafios_Desafio040.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Code

Python example

    cores = {'Limpa':'\033[m', 'Negrito':'\033[1m', 'Azul/Negrito':'\033[1;34m'}
    
    print('Crie um programa que leia duas notas de um aluno e calcule sua média, mostrando uma mensagem no final,\nde acordo com a média atingida:'
          '\n- Média abaixo de {}5.0{}: {}REPROVADO{}'
          '\n- Média entre {}5.0{} e {}6.9{}: {}RECUPERAÇÃO{}'
          '\n- Média {}7.0{} ou superior: {}APROVADO{}\n'.format(cores['Negrito'], cores['Limpa'], cores['Azul/Negrito'], cores['Limpa'], cores['Negrito'], cores['Limpa'], cores['Negrito'], cores['Limpa'], cores['Azul/Negrito'], cores['Limpa'],cores['Negrito'], cores['Limpa'], cores['Azul/Negrito'],cores['Limpa']))
    
    nota1 = float(input('Informe a primeira nota: '))
    nota2 = float(input('Informe a segunda nota: '))
    
    n = float(5.9)
    
    if (nota1 + nota2)/ 2 >= 7.0:
        print('Sua média foi {} e você está {}APROVADO{}!'.format((nota1+nota2)/2, cores['Negrito'], cores['Limpa']))
    elif (nota1 + nota2)/ 2 <= 6.9 and (nota1+nota2)/2 >= 5.0:
        print('Sua média foi {} e você está de {}RECUPERAÇÃO{}.'.format((nota1+nota2)/2, cores['Negrito'], cores['Limpa']))
    else:
        print('Sua média foi {} e você está {}REPROVADO{}.'.format((nota1+nota2)/2, cores['Negrito'], cores['Limpa']))

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: Mundo_2_Desafios_Desafio056
date: 2020-05-07
---
Example Python program Mundo_2_Desafios_Desafio056.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Code

Python example

    print('Desenvolva um programa que leia o nome, idade e sexo de 4 pessoas. No final do programa, mostre:'
          '\nA média de idade do grupo'
          '\nQual é o nome do homem mais velho do'
          '\nQuantas mulheres têm menos de 20 anos\n')
    
    maiorIdade = 0
    menorIdade = 0
    mediaIdade = 0
    maisVelho = str
    
    for c in range(0,4):
        nome = str(input('Informe o seu nome: '))
        idade = int(input('Informe a sua idade: '))
        sexo = str(input('Informe o seu genero entre: Masculino e Feminino: ')).lower()
        if idade > maiorIdade and sexo == 'masculino':
            maiorIdade = idade
            maisVelho = nome
        elif idade <= 20 and sexo == 'feminino':
            menorIdade += 1
        mediaIdade += idade
    
    print('A idade média do grupo é de: {}'
          '\nO nome do homem mais velho é: {}'
          '\nA quantidade de mulheres com menos de 20 anos é: {}'.format(mediaIdade/2, maisVelho, menorIdade))

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

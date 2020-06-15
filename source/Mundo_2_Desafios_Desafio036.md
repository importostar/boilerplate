---
title: Mundo_2_Desafios_Desafio036
date: 2020-05-07
---
Example Python program Mundo_2_Desafios_Desafio036.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Code

Python example

    print('Escreva um programa para aprovar o empréstimo bancário para a compra de uma casa. O programa vai perguntar:\n'
          '-O valor da casa'
          '\n-O salário do comprador '
          '\n-Quantos anos ele pretende pagar'
          '\nCalcule o valor da prestação mensal, sabendo que não pode exceder 30% do salário ou então o emprestimo será negado.')
    
    valor_casa = float(input('\nInforme o valor do imovel: '))
    salario = float(input('Informe o salário: '))
    anos = int(input('Informe em quantos anos será pago: '))
    
    quant_prest = anos * 12
    prest_mensal = valor_casa/quant_prest
    
    if salario * 0.3 > prest_mensal:
        print('\n\nSeu empréstimo bancário foi aprovado!!')
        print('Você pagará {} prestações de R${:.2f} por {} anos'.format(quant_prest, prest_mensal, anos))
    
    else:
        print('Infelizmente você não foi aprovado para o empréstimo, sentimos muito.')

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

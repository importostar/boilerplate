---
title: Mundo_2_Desafios_Desafio044
date: 2020-05-07
---
Example Python program Mundo_2_Desafios_Desafio044.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Code

Python example

    print('Elabore um programa que calcule o valor a ser pago por um produto considerando o seu PREÇO NORMAL e CONDIÇÃO DE\nPAGAMENTO:'
          '\n- à vista dinheiro/cheque: 10% de desconto'
          '\n- à vista no cartão: 5% de desconto'
          '\n- em até 2x no cartão:  preço normal'
          '\n- 3x ou mais no cartão: 20% de juros no valor total\n')
    
    preco = float(input('Informe o valor do produto: R$'))
    pagamento = float(input('Escolha entre as formas de pagamento abaixo:'
                            '\n1- à vista dinheiro/cheque: 10% de desconto'
                            '\n2- à vista no cartão: 5% de desconto'
                            '\n3- em até 2x no cartão:  preço normal'
                            '\n4- 3x ou mais no cartão: 20% de juros no valor total\n'
                            'Método de pagamento: '))
    
    if pagamento == 1:
        print('O valor do produto ficará: R${:.2f}'.format(preco-(preco*0.1)))
    elif pagamento == 2:
        print('O valor do produto ficará: R${:.2f}'.format(preco-(preco*0.05)))
    elif pagamento == 3:
        print('O preço do produto continuará R${:.2f}'.format(preco))
    elif pagamento == 4:
        print('O preco do produto ficará: R${:.2f}'.format(preco+(preco*0.2)))
    else:
        print('Essa não é uma forma válida de pagamento.')
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

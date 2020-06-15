---
title: Mundo_2_Desafios_Desafio039
date: 2020-05-07
---
Example Python program Mundo_2_Desafios_Desafio039.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from datetime import date

## Code

Python example

    from datetime import date
    cores = {'Limpa':'\033[m', 'Negrito':'\033[1m'}
    
    print('\nFaça um programa qu eleia o ano de nascimento e um jovem e informe, de acordo com sua idade:'
          '\n- Se ele{} ainda vai se alistar {}no serviço militar.'
          '\n- Se é a{} hora de se alistar{}.'
          '\n- Se já{} passou do tempo{} do alistamento.'
          '\nSeu programa também deverá mostrar o tempo que falta ou que passou do prazo.'.format(cores['Negrito'], cores['Limpa'], cores['Negrito'], cores['Limpa'], cores['Negrito'], cores['Limpa']))
    
    ano = int(input('\nInforme o ano de seu nascimento: '))
    calc_idade = date.today().year - ano
    
    if calc_idade < 18:
        print('\nVocê ainda não precisa se alistar nas forças armadas, em {} anos você deverá se alistar.'.format(18 - calc_idade))
    elif calc_idade == 18:
        print('\nVocê deve se apresentar na junta mais próxima antes de Junho.')
    else:
        print('\nVocê já passou do tempo de alistamento em {} anos, se apresente na junta mais próxima para mais informações.'.format(calc_idade - 18))
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: Operacoes (1)
date: 2020-05-07
---
Example Python program Operacoes (1).py

## Modules

* from math import sqrt
* import sys

## Classes

* class Operacoes:

## Methods

* def __init__(self, entrada, saida):
* def set_entrada(self, simbolo):
* def botao_0(self):
* def botao_ponto(self):
* def botao_modulo(self):
* def botao_mais(self):
* def botao_igual(self):
* def botao_AC(self):
* def botao_1(self):
* def botao_2(self):
* def botao_3(self):
* def botao_menos(self):
* def botao_ao_quadrado(self):
* def botao_sqrt(self):
* def botao_4(self):
* def botao_5(self):
* def botao_6(self):
* def botao_multiplicar(self):
* def botao_parenteses_abrindo(self):
* def botao_parenteses_fechando(self):
* def botao_7(self):
* def botao_8(self):
* def botao_9(self):
* def botao_divisao(self):
* def botao_exit(self):
* def botao_del(self):

## Code

Python example

    from math import sqrt
    import sys
    
    class Operacoes:
        '''
        Define o que cada botão deverá fazer
        '''
        def __init__(self, entrada, saida):
            '''
            Recebe dois stringVars, um da entrada e outro da tela de resultados
            '''
            self.entrada = entrada
            self.resultado = saida
    
        def set_entrada(self, simbolo):
            self.entrada.set(self.entrada.get()+simbolo)
    
        def botao_0(self):
            self.set_entrada('0')
    
        def botao_ponto(self):
            self.set_entrada('.')
    
        def botao_modulo(self):
            self.set_entrada('%')
    
        def botao_mais(self):
            self.set_entrada('+')
    
        def botao_igual(self):
            try:
                self.resultado.set(eval(self.entrada.get()))
                self.entrada.set("")
            except:
                self.resultado.set("ERRO!")
                self.entrada.set("")
        def botao_AC(self):
            self.entrada.set("")
            self.resultado.set("")
    
        def botao_1(self):
            self.set_entrada('1')
    
        def botao_2(self):
            self.set_entrada('2')
    
        def botao_3(self):
            self.set_entrada('3')
    
        def botao_menos(self):
            self.set_entrada('-')
    
        def botao_ao_quadrado(self):
            self.set_entrada('**2')
    
        def botao_sqrt(self):
            self.set_entrada('sqrt(')
    
        def botao_4(self):
            self.set_entrada('4')
    
        def botao_5(self):
            self.set_entrada('5')
    
        def botao_6(self):
            self.set_entrada('6')
    
        def botao_multiplicar(self):
            self.set_entrada('*')
    
        def botao_parenteses_abrindo(self):
            self.set_entrada('(')
    
        def botao_parenteses_fechando(self):
            self.set_entrada(')')
    
        def botao_7(self):
            self.set_entrada('7')
    
        def botao_8(self):
            self.set_entrada('8')
    
        def botao_9(self):
            self.set_entrada('9')
    
        def botao_divisao(self):
            self.set_entrada('/')
    
        def botao_exit(self):
            sys.exit()
            
        def botao_del(self):
            entrada = self.entrada.get()
            self.entrada.set(entrada[:(len(entrada) - 1)])
            del entrada
    
    
        
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

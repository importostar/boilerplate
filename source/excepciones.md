---
title: excepciones
date: 2020-05-07
---
Example Python program excepciones.py
For Python version 2.x.
To test your Python version use:

    python --version


## Methods

* def division_cero():
* def error_tipo():
* def funcion_no_existe():
* def nombre_no_definido():
* def una_excepcion():
* def archivo_no_existe():
* def archivo_no_encontrado():
* def excepciones_sintaxis_division():
* def introduce_edad(edad):
* def clase_no_definida():
* def main():

## Code

Python example

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    
    #Try Except
    # https://thepythonguru.com/python-exception-handling/
    
    def division_cero():
        print("#Funcion > Division por cero")
        try:
            numero = 9 / 0.0
        except ZeroDivisionError:
            print("No puedes dividir entre cero")
    
    
    def error_tipo():
        print("#Funcion > Error de tipos")
        try:
            numero = float("34F")
        except ValueError:
            print("El tipo es erroneo: No puedes convertir un str a float")
    
    
    def funcion_no_existe():
        print("#Funcion > Exception")
        try:
            no_existe(33,101)
        except:
            print("Ha ocurrido una excepcion: la función 'noexiste' no esta definida ")
        finally:
            print("Fin")
    
    def nombre_no_definido():
        print("#Funcion > Nombre no definido")
        try:
            print(x)
        except NameError:
            print("La variable 'x' no esta definida")
        except:
            print("-")
    
    def una_excepcion():
        print("#Funcion > una excepcion que no ocurre")
        try:
            print("Hola, mundo!")
        except:
            print("Ha ocurrido una Exception")
        else:
            print("Ninguna Exception ha ocurrido")
    
    
    def archivo_no_existe():
        print("#Funcion > archivo no existe")
        try:
            file = open("noexiste.dat","r")
        except FileNotFoundError:
            print("El archivo 'noexiste.dat' no existe")
        finally:
            print("Ha finalizado el programa")
    
    
    def archivo_no_encontrado():
        print("#Funcion > archivo no encontrado")
        try:
            f = open('noexiste.txt', 'r')
            print(f.read())
            f.close()
        except IOError:
            print("El archivo 'noexiste.txt' no existe")
        finally:
            print("Fin del programa")
    
    
    def excepciones_sintaxis_division():
        print("#Funcion > errores de sintaxis o division por cero")
        try:
            num1, num2 = eval(input("Introduce dos numeros separados por coma : "))
            result = num1 / num2
            print("El resultado de la división es ", result)
        except ZeroDivisionError:
            print("Ha ocurrido una excepcion: División por cero")
        except SyntaxError:
            print("Error de sintaxis: los números deben estar separados por coma")
        except:
            print("entrada erronea")
        else:
            print("No ocurrio ninguna excepción")
        finally:
            print("Ha finalizado el programa")
    
    
    
    def introduce_edad(edad):
        print("#Funcion > introduce edad")
        if edad < 0:
            raise ValueError("Error de valor: Solo introduce número")
        if edad % 2 == 0:
            print("Alfa:",edad)
        else:
            print("Gama:",edad)
    
    
    def clase_no_definida():
        print("#Funcion > clase no definida")
        try:
            extractor = Extractor()
        except NameError as ex:
            print("Ha ocurrido una excepción: tipo no definido, ",ex)
    
    
    def main():
        division_cero()
        error_tipo()
        funcion_no_existe()
        nombre_no_definido()
        una_excepcion()
        archivo_no_existe()
        archivo_no_encontrado()
        excepciones_sintaxis_division()
        try:
            tuedad= int(input("Introduce edad: "))
            introduce_edad(tuedad)
        except ValueError:
            print("Error de valor: solo números enteros positivos ")
        except:
            print("Ha ocurrido una excepción")
        finally:
            print("Ha terminado !!")
    
        clase_no_definida()
    
    
    
    if __name__ == '__main__':
        main()
        
    '''
    except IOError:
        print('An error occured trying to read the file.')
        
    except ValueError:
        print('Non-numeric data found in the file.')
    
    except ImportError:
        print "NO module found"
        
    except EOFError:
        print('Why did you do an EOF on me?')
    
    except KeyboardInterrupt:
        print('You cancelled the operation.')
    
    except:
        print('An error occured.')
    '''

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

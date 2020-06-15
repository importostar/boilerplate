---
title: converter (1)
date: 2020-05-07
---
Example Python program converter (1).py

## Modules

* from math import ceil, floor
* from string import ascii_lowercase, ascii_uppercase, digits
* from typing import Tuple, Union

## Methods

* def mod(dividend: int, divisor: int) -> Tuple[int, int]:
* def to_decimal(number: str, base: Union[int, str], table: str = DEFAULT_TABLE) -> Union[int, float]:
* def to_base(number: Union[int, float], base: Union[int, str], table: str = DEFAULT_TABLE) -> str:
* def convert(number: str, original_base: Union[int, str] = 0, result_base: Union[int, str] = 10,

## Code

Python example

    #!/usr/bin/env python3.8
    # -*- coding: utf-8 -*-
    
    __all__ = ['mod', 'to_decimal', 'to_base', 'convert', 'DEFAULT_TABLE']
    
    from math import ceil, floor
    from string import ascii_lowercase, ascii_uppercase, digits
    from typing import Tuple, Union
    
    DEFAULT_TABLE = digits + ascii_uppercase + ascii_lowercase
    
    
    def mod(dividend: int, divisor: int) -> Tuple[int, int]:
        quotient, remainder = dividend // divisor, dividend % divisor
        if remainder < 0:
            quotient += 1
            remainder -= divisor
        return quotient, remainder
    
    
    def to_decimal(number: str, base: Union[int, str], table: str = DEFAULT_TABLE) -> Union[int, float]:
        base = int(base)
    
        position = number.find('.')
    
        if number[0] == '-':
            negative = True
            number = number[1:]
        else:
            negative = False
    
        if position == -1:
            result, index = 0, 1
            for digit in number[::-1]:
                result += index * table.find(digit)
                index *= base
        else:
            integer, fraction = number.split('.')
            result, index = to_decimal(integer, base, table), 1.0
            for digit in fraction:
                index /= base
                result += index * table.find(digit)
    
        return -result if negative else result
    
    
    def to_base(number: Union[int, float], base: Union[int, str], table: str = DEFAULT_TABLE) -> str:
        try:
            base = int(base)
        except ValueError:
            pass
    
        if number == 0:
            return table[0] if isinstance(number, int) else '{}.{}'.format(table[0], table[0])
    
        result_numbers = []
        if number < 0 < base:
            negative = True
            number = abs(number)
        else:
            negative = False
    
        if isinstance(number, int):
            while number != 0:
                number, remainder = mod(number, base)
                result_numbers.insert(0, table[remainder])
        else:
            integer = ceil(number) if base < 0 else floor(number)
            fraction = number - integer
            result_numbers.append(to_base(integer, base, table) + '.')
            times = 0
            while fraction != 0 and times < 100:
                fraction *= base
                integer = ceil(fraction) if base < 0 else floor(fraction)
                fraction -= integer
                result_numbers.append(table[integer])
                times += 1
            if times == 0:
                result_numbers.append(table[0])
    
        if negative:
            result_numbers.insert(0, '-')
        return ''.join(result_numbers)
    
    
    def convert(number: str, original_base: Union[int, str] = 0, result_base: Union[int, str] = 10,
                table: str = DEFAULT_TABLE) -> str:
        original_base, result_base = int(original_base), int(result_base)
        if original_base == result_base:
            return number
        return to_base(to_decimal(number, original_base, table), result_base, table)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

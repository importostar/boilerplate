---
title: week2_week2_3
date: 2020-05-07
---
Example Python program week2_week2_3.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Code

Python example

    string = "브이넥 라이트 다운 베스트"
    string1= "    25,900원"
    
    #인덱싱
    print(string[0])
    print(string[2])
    print(string[3])
    print(string[-1])
    print(string[-3])
    #print(string[14])
    
    #슬라이싱(<= : <)
    print(string[0:2])
    print(string[0:3])
    print(string[-3:-1])
    print(string[11:])
    print(string[:6])
    print(string[:])
    
    #문자열 변환
    print(string.replace("라이트", "헤비"))
    print(string)
    string = string.replace("라이트", "헤비")
    print(string)
    
    #공백제거
    print(string1.strip())
    string1 = string1.strip()  #공백제거
    string1 = string1.replace(",", "")
    string1 = string1[:-1]
    print(string1)
    plusone = int(string1) + 1
    print(plusone)
    
    #함수체이닝
    string1 = string1.strip().replace(",", "")[:-1]
    print(string1)
    
    #리스트
    players = ["황의조", "황희찬", "구자철", "이재성", "기성용"]
    
    small_players = players[1:3]
    print(small_players)
    
    small_players = players[-4:-1]
    print(small_players)
    
    small_players = players[3:]
    print(small_players)
    
    small_players = players[:4]
    print(small_players)
    
    players.append("이승우")
    print(players)
    players.append("김민재")
    print(players)
    
    del players[1]
    del players[1]
    
    print(players)
    print(len(players))

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

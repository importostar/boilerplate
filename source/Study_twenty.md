---
title: Study_twenty
date: 2020-05-07
---
Example Python program Study_twenty.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import random

## Code

Python example

    import random
    
    list0 = ['<힘 내>','<소원을 말해봐>','<I Got A Boy>','<Lion Heart>','멤버 중 한 명이 최근에 발표한 곡은 <사계>입니다.','이들의 팬을 <소원>이라고 부릅니다.','걸그룹으로, 2007년 데뷔했습니다.','원더걸스와 함께 가요계를 주름잡았습니다.','SM 이수만 회장의 조카가 소속되어 있습니다.','멤버는 9명이었으나 8명으로 재편되었습니다.','히트곡은 <Gee>입니다.']
    list1 = ['<그날의 너>','<찾아가세요>','<종소리>','이들의 팬을 <러블리너스>라고 부릅니다.','멤버 중 한 명의 본명은 김지연입니다.','걸그룹으로, 2014년 데뷔했습니다.','멤버가 8명입니다.','2016년 고려대학교 대동제 무대에 섰습니다.','리더와 막내의 나이차는 6년입니다.','캐나다 여행 프로그램을 촬영했던 적이 있습니다.']
    list2 = ['<소중한 사랑>을 2016년에 리메이크했습니다.','<Heart Shaker>','<올해 제일 잘한 일>','이들의 팬을 <원스>라고 부릅니다.','멤버 중 한 명의 본명은 유정연입니다.','걸그룹으로, 2015년 데뷔했습니다.','멤버가 9명입니다.','2019년 연세대학교 아카라카 무대에 섰습니다.','멤버 중 한국인은 5명입니다.', '일본에서 인기를 얻고 있습니다.','박진영의 프로듀싱 아래 데뷔했습니다.']
    list3 = ['<작은 것들을 위한 시>','<I NEED YOU>','<피 땀 눈물>','<전하지 못한 진심>','이들의 팬을 <아미>라고 부릅니다.','알파벳 세 글자로 줄여 부릅니다.','멤버 중 한 명의 본명은 김남준입니다.','보이그룹으로, 2013년 데뷔했습니다.','멤버가 7명입니다.','유튜브 스타로 유명합니다.','해외 유명 가수인 Hasley와 작업했습니다.','2019년 고려대학교 입실렌티에 올지 안 올지는 모릅니다.']
    
    superlist = [list0, list1, list2, list3]
    answer = ['소녀시대','러블리즈','트와이스','방탄소년단']
    
    random.shuffle(list0)
    random.shuffle(list1)
    random.shuffle(list2)
    random.shuffle(list3)
    
    list = random.choice(superlist)
    index = 0
    
    for j in range(len(superlist)):
        if (superlist[j]==list):
            index = j
            break
    
    for i in list:
        print(i)
        k = input('가수이름>').strip()
        if (k==answer[index]):
            print('정답입니다.')
            break
        else:
            print('오답입니다.')
            continue
    
    print('정답은',answer[index],'입니다.')
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: list_diff
date: 2020-05-07
---
Example Python program list_diff.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Methods

* def list_diff(l1, l2):

## Code

Python example

    """
    重複を殺して良いなら Set にして
    差を求めるのもアリ
    """
    set1 = set(['A', 'B'])
    set2 = set(['A'])
    
    set1 - set2  # {'B'}  ... set1 にしかないやつ
    set2 - set1  # set() ... set2 にしかないやつ
    
    set1 | set2  # {'A', 'B'} ... 両方を合算
    set1 & set2  # {'A'} ... 両方にあるやつ
    
    """
    重複データを含めた、完全な差分を求める場合は適当に回さないとむり
    @ref https://dot-blog.jp/news/python-two-list-difference/
    """
    def list_diff(l1, l2):
        if len(l1) >= len(l2):
            diff = l1.copy()
            comp = l2.copy()
        else:
            diff = l2.copy()
            comp = l1.copy()
        for v in comp:
            if v in diff:
                diff.remove(v)
            else:
                diff.append(v)
        return diff
    
    l1 = ['大山', '佐藤', '大山', '佐藤', '山下', '平野', '山下', '平野']
    l2 = ['大山', '佐藤']
    
    result = list_diff(l1, l2)
    print(result)
    
    # 出力は ['大山', '佐藤', '山下', '平野', '山下', '平野'] となり
    # 完全に同じである最初の '大山', '佐藤', セット以外が全て差分として抽出される

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

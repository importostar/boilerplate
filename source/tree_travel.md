---
title: tree_travel
date: 2020-05-07
---
Example Python program tree_travel.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Classes

* class TreeNode:

## Methods

* def __init__(self, x):
* def front_travel(root):
* def mid_travel(root):
* def post_travel(root):

## Code

Python example

    class TreeNode:
        def __init__(self, x):
            self.val = x
            self.left = None
            self.right = None
            
    def front_travel(root):
        if not root: return
        s = [root]
        while s:
            cur = s.pop()
            print(cur.val)
    
            if cur.right:
                s.append(cur.right)
            if cur.left:
                s.append(cur.left)
    
    def mid_travel(root):
        if not root: return
        cur, s = root, []
        while cur or s:
            while cur:
                s.append(cur)
                cur = cur.left
    
            cur = s.pop()
            print(cur.val)
            cur = cur.right
    
    def post_travel(root):
        if not root: return
        s = [(0, root)]
        while s:
            seen, cur = s.pop()
            if not cur: continue
    
            if seen:
                print(cur.val)
            else:
                s.append((1, cur))
                s.append((0, cur.right))
                s.append((0, cur.left))

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

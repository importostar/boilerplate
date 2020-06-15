---
title: bst
date: 2020-05-07
---
Example Python program bst.py


## Classes

* class Node:
* class BSTTree:

## Methods

* def reversePairs_using_bst_tree(nums):
* def __init__(self, v, left=None, right=None):
* def __init__(self):
* def insert(self, v):
* def _insert_dfs(self, root, v):
* def search(self, v):
* def _search_impl(self, root, v):

## Code

Python example

    def reversePairs_using_bst_tree(nums):
        class Node:
            def __init__(self, v, left=None, right=None):
                self.val = v
    
                # cnt初始值为1，因为节点本身记录cnt，创建的时候就包含了一次
                # cnt记录大于等于v的节点个数
                self.cnt = 1
                self.left = left
                self.right = right
    
        class BSTTree:
            def __init__(self):
                self.root = None
    
            def insert(self, v):
                self.root = self._insert_dfs(self.root, v)
    
            # BST实现时候的尾递归技巧，将root传入，然后返回当前insert之后的root
            # 如果root是空，创建节点，上层可以得到最新的root。如果不是，根据节点关系，递归构造，同时维护left和right的关系，最后返回root
            # 注意这里保存的cnt表示大于等于当前节点的个数。如果只是大于，会存在问题，比如搜索大于4的，结果搜索到节点是5，但是5自身的数值无法记录。
            # 所以BST记录数据**一定要保存自己的数值**
            def _insert_dfs(self, root, v):
                if not root:
                    return Node(v)
                elif root.val == v:
                    root.cnt += 1
                elif root.val < v:
                    root.cnt += 1
                    root.right = self._insert_dfs(root.right, v)
                else:
                    root.left = self._insert_dfs(root.left, v)
    
                return root
    
            def search(self, v):
                return self._search_impl(self.root, v)
    
            # 搜索的时候，如果是左节点，需要加上当前的数值，因为当前根节点和右节点都大于当前数值。
            def _search_impl(self, root, v):
                if not root:
                    return 0
                elif root.val == v:
                    return root.cnt
                elif root.val < v:
                    return self._search_impl(root.right, v)
                else:
                    return root.cnt + self._search_impl(root.left, v)
    
        # 搜索使用2*v+1
        res, tree = 0, BSTTree()
        for v in nums:
            res += tree.search(2*v+1)
            tree.insert(v)
    
        return res

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

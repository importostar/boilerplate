---
title: pengxiang_hua_utlities_heap
date: 2020-05-07
---
Example Python program pengxiang_hua_utlities_heap.py


## Classes

* class PriorityQueueBase:
* class Item:
* class HeapPriorityQueue (PriorityQueueBase):

## Methods

* def __init__(self, v):
* def __lt__(self, other):  # 比较大小
* def is_empty(self):
* def __str__(self):
* def __init__(self):
* def __len__(self):
* def is_empty(self):
* def add(self, value):  # 在后面加上然后加上
* def min(self):
* def remove_min(self):
* def _parent(self, j):
* def _left(self, j):
* def _right(self, j):
* def _has_left(self, j):
* def _has_right(self, j):
* def _swap(self, i, j):
* def _upheap(self, j):  # 往上交换
* def _downheap(self, j):  # 往下交换，递归比较三个值

## Code

Python example

    # 该heap为min_heap，即根节点为最小值,依据第三项元素的值
    class PriorityQueueBase:
        # 抽象基类为堆
    
        class Item:
            # 轻量级组合来存储堆项目
            __slots__ = 'a', 'b','c'
    
            def __init__(self, v):
                self.a = v[0]
                self.b = v[1]
                self.c = v[2]
    
            def __lt__(self, other):  # 比较大小
                return self.c < other.c
    
            def is_empty(self):
                return len (self) == 0
    
            def __str__(self):
                return str ([self.a,self.b,self.c])
    
    class HeapPriorityQueue (PriorityQueueBase):
    
        def __init__(self):
            self._data = []
    
        def __len__(self):
            return len (self._data)
    
        def is_empty(self):
            return len (self) == 0
    
        def add(self, value):  # 在后面加上然后加上
            self._data.append (self.Item (value))
            self._upheap (len (self._data) - 1)
    
        def min(self):
            if self.is_empty ():
                raise ValueError ("Priority queue is empty.")
            item = self._data[0]
            return [item.a, item.b, item.c]
    
        def remove_min(self):
            if self.is_empty ():
                raise ValueError ("Priority queue is empty.")
            self._swap (0, len (self._data) - 1)
            item = self._data.pop ()
            self._downheap (0)
            return [item.a, item.b, item.c]
    
        def _parent(self, j):
            return (j - 1) // 2
    
        def _left(self, j):
            return 2 * j + 1
    
        def _right(self, j):
            return 2 * j + 2
    
        def _has_left(self, j):
            return self._left (j) < len (self._data)
    
        def _has_right(self, j):
            return self._right (j) < len (self._data)
    
        def _swap(self, i, j):
            self._data[i], self._data[j] = self._data[j], self._data[i]
    
        def _upheap(self, j):  # 往上交换
            parent = self._parent (j)
            if j > 0 and self._data[j] < self._data[parent]:
                self._swap (j, parent)
                self._upheap (parent)
    
        def _downheap(self, j):  # 往下交换，递归比较三个值
            if self._has_left (j):
                left = self._left (j)
                small_child = left
                if self._has_right (j):
                    right = self._right (j)
                    if self._data[right] < self._data[left]:
                        small_child = right
                if self._data[small_child] < self._data[j]:
                    self._swap (j, small_child)
                    self._downheap (small_child)
    
    if __name__ == '__main__':
        heap = HeapPriorityQueue ()
        heap.add ([0, 1, 1])
        heap.add ([1, 1, 0.9])
        heap.add ([2, 1, 0.2])
        heap.add ([3, 1, 0.5])
        heap.add ([4, 1, 0.4])
        heap.add ([5, 1, 0.7])
        heap.add ([6, 1, 0.8])
        heap.add ([7, 1, 0.6])
    
        for item in heap._data:
            print (item)
    
        print ("min is: ")
        print (heap.min ())
        print ()
    
        print ("remove min: ")
        print (heap.remove_min ())
        print ("Now min is: ")
        print (heap.min ())
        print ()
    
        print ("remove min: ")
        print (heap.remove_min ())
        print ("Now min is: ")
        print (heap.min ())
        print ()
    
        heap.add ([1, 2, 0.01])
        print ("Now min is: ")
        print (heap.min ())
        print ()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

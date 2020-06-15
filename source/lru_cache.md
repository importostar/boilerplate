---
title: lru_cache
date: 2020-05-07
---
Example Python program lru_cache.py


## Classes

* class LinkedNode:
* class LRUCache:

## Methods

* def __init__(self, value, next):
* def __init__(self, capacity):
* def get(self, key):
* def put(self, key, value):
* def _insert_impl(self, new_node):

## Code

Python example

    class LinkedNode:
        def __init__(self, value, next):
            self.value = value
            self.next = next
    
    
    class LRUCache:
        def __init__(self, capacity):
            self.head = LinkedNode(None, None)
            self.tail = None
            self.node_pre_map = {}
            self.capacity = capacity
    
        def get(self, key):
            if key not in self.node_pre_map: return -1
    
            # remove node
            pre = self.node_pre_map.pop(key)
            pre.next, cur = pre.next.next, pre.next
            if not cur.next: self.tail = pre
    
            # insert node to front
            self._insert_impl(cur)
            return cur.value[1]
    
        def put(self, key, value):
            if key in self.node_pre_map: return
            if len(self.node_pre_map) == self.capacity:
                if not self.tail: return
                self.tail = self.node_pre_map.pop(self.tail.value[0])
                self.tail.next = None
            self._insert_impl(LinkedNode((key, value), None))
    
        def _insert_impl(self, new_node):
            new_node.next = self.head.next
            self.head.next = new_node
            self.node_pre_map[new_node.value[0]] = self.head
    
            if new_node.next:
                self.node_pre_map[new_node.next.value[0]] = new_node
            else:
                self.tail = new_node

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

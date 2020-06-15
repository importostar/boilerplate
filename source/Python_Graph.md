---
title: Python_Graph
date: 2020-05-07
---
Example Python program Python_Graph.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import queue

## Classes

* class Stack:

## Methods

* def __init__(self):
* def empty(self):
* def push(self, p):
* def pop(self):
* def depth(node):
* def width(node):
* def reset():

## Code

Python example

    import queue
    
    
    class Stack:
        def __init__(self):
            self.__storage = []
    
        def empty(self):
            return len(self.__storage) == 0
    
        def push(self, p):
            self.__storage.append(p)
    
        def pop(self):
            return self.__storage.pop()
    
    graph = {}
    vertexes = []
    wayDepth = []
    wayWidth = []
    stack = Stack()
    myqueue = queue.Queue()
    
    
    def depth(node):
        global graph
        global stack
        graph[node][1] = 'Black'
        stack.push(node)
        print('Depth search. Working on node ' + node + ". It's now " + graph[node][1] + ' node.')
        wayDepth.append(node)
        for j in range(0, len(graph[node][0])):
            if not stack.empty():
                if graph[graph[node][0][j]][1] == 'Gray':
                    depth(graph[node][0][j])
        stack.pop()
    
    
    def width(node):
        global graph
        global myqueue
        graph[node][1] = 'Black'
        myqueue.put(node)
        print('Width search. Working on node ' + node + ". It's now " + graph[node][1] + ' node.')
        wayWidth.append(node)
        while not myqueue.empty():
            temp = myqueue.get()
            for j in range(0, len(graph[temp][0])):
                print('Width search. Working on node ' + graph[temp][0][j] +
                      ". It's " + graph[graph[temp][0][j]][1] + ' node.')
                if graph[graph[temp][0][j]][1] == 'Gray':
                    graph[graph[temp][0][j]][1] = 'Black'
                    print("Now it's " + graph[graph[temp][0][j]][1] + ' node.')
                    myqueue.put(graph[temp][0][j])
                    wayWidth.append(graph[temp][0][j])
    
    
    def reset():
        global graph
        global wayDepth
        global wayWidth
        wayDepth.clear()
        wayWidth.clear()
        for node in range(65, len(graph) + 65):
            graph[chr(node)][1] = 'Gray'
    
    # Ввод графа
    character = 65
    for i in range(0, int(input('Input graph length >> '))):
        graph[chr(character)] = []
        character += 1
    for i in range(65, len(graph) + 65):
        elList = []
        curList = []
        for j in range(0, int(input('Number of edges from node ' + chr(i) + ': '))):
            curList.append(input('Node ' + chr(i) + ' to node '))
        elList.append(curList)
        elList.append('Gray')
        graph[chr(i)] = elList.copy()
    print('==============')
    for i in range(65, len(graph) + 65):
        print(chr(i) + ' is ' + graph[chr(i)][1])
        for j in range(0, len(graph[chr(i)][0])):
            print('-> ' + graph[chr(i)][0][j])
        print('==============')
    # Конец ввода графа
    
    sw = True
    while sw:
        reset()
        sas = input('Start search from node ')
        depth(sas)
        print(wayDepth)
        reset()
        width(sas)
        print(wayWidth)
        sw = input('Do it again? (y/n) >> ') == 'y'
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

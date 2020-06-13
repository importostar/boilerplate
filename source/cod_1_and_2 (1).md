---
title: cod_1_and_2 (1)
date: 2020-05-07
---
Example Python program cod_1_and_2 (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Methods

* def dfs(start, visited=[]):
* def bfs(start, end):

## Code

Python example

     # cod 1:
    
    # https://docs.python.org/2/tutorial/datastructures.html#dictionaries
    grap = {0: [1], 1: [0, 2], 2: [1], 3: [1, 4], 4: [3]}
    
    
    # https://docs.python.org/2/tutorial/controlflow.html#defining-functions
    def dfs(start, visited=[]):
        # https://docs.python.org/2/tutorial/introduction.html#lists
        visited.append(start)
    
        # https://docs.python.org/2/tutorial/controlflow.html#for-statements
        for i in grap.get(start):
    
            # https://docs.python.org/2/tutorial/controlflow.html#if-statements
            if i not in visited:
                dfs(i, visited)
        return visited
    
    # https://docs.python.org/3.3/library/functions.html?highlight=print#print
    print(dfs(4))
    
    # cod 2:
    
    # https://docs.python.org/2/tutorial/datastructures.html#dictionaries
    graph = {0:[1], 1:[0,2], 2:[1], 3:[1,4], 4:[3]}
    
    # https://docs.python.org/2/tutorial/controlflow.html#defining-functions
    def bfs(start, end):
        # https://docs.python.org/2/tutorial/introduction.html#lists
        queue = [[start]]
        # https://docs.python.org/2/tutorial/datastructures.html#sets
        visited = set()
    
        # https://docs.python.org/2/tutorial/controlflow.html#break-and-continue-statements-and-else-clauses-on-loops
        while queue:
            # https://docs.python.org/3.3/tutorial/datastructures.html#using-lists-as-queues
            path = queue.pop(0)
    
            v = path[-1]
    
            # https://docs.python.org/2/tutorial/controlflow.html#if-statements
            if v == end:
                return path
            elif v not in visited:
                for vizinho in graph.get(v):
                    # https://docs.python.org/2/tutorial/introduction.html#lists
                    new_path = list(path)
                    new_path.append(vizinho)
                    queue.append(new_path)
                    print(queue)
                visited.add(v)
    
    # https://docs.python.org/3.3/library/functions.html?highlight=print#print
    print(bfs(1,4))

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

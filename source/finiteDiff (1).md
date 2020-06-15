---
title: finiteDiff (1)
date: 2020-05-07
---
Example Python program finiteDiff (1).py

## Modules

* import numpy
* import matplotlib.pyplot

## Classes

* class System:

## Methods

* def __init__(self,length,height,gridSize):
* def plot(self,name):
* def plotConvergence(self,name):
* def boundaryInit(self, north, east, west, south):
* def iterate(self,fittingFactor=1):
* def solve(self, prec,fittingFactor=1):

## Code

Python example

    import numpy
    import matplotlib.pyplot
    
    class System:
        def __init__(self,length,height,gridSize):
            self.length = length
            self.height = height
            self.gridSize = gridSize
            self.grid = numpy.empty((self.height/self.gridSize + 1, self.length/self.gridSize + 1,))
            self.__str__ = self.grid.__str__
        def plot(self,name):
            matplotlib.pyplot.clf()
            matplotlib.pyplot.imshow(self.grid, cmap='cool', interpolation='nearest')
            matplotlib.pyplot.savefig(name)
        def plotConvergence(self,name):
            matplotlib.pyplot.clf()
            matplotlib.pyplot.plot(sys.errorHistory[1:])
            matplotlib.pyplot.savefig(name)
        def boundaryInit(self, north, east, west, south):
            self.grid[:] = min([north,east,west,south])
            self.grid[0,] = north
            self.grid[self.height/self.gridSize] = south
            self.grid[:,0] = west
            self.grid[:,self.length/self.gridSize] = east
        def iterate(self,fittingFactor=1):
            self.it += 1
            for i in xrange(1,int(self.height/self.gridSize)):
                for j in xrange(1, int(self.length/self.gridSize)):
                    new = (self.grid[i+1,j] + self.grid[i,j+1] + self.grid[i-1,j] + self.grid[i,j-1])/4.0
                    self.grid[i,j] = self.grid[i,j] + (new - self.grid[i,j])*fittingFactor
        def solve(self, prec,fittingFactor=1):
            self.it = 0
            oldSum = numpy.sum(abs(self.grid[1:self.height/self.gridSize, 1:self.length/self.gridSize]))
            newSum = 123
            self.errorHistory = []
            while True:
                oldSum = newSum
                self.iterate(fittingFactor)
                newSum = numpy.sum(abs(self.grid[1:self.height/self.gridSize, 1:self.length/self.gridSize]))
                error = abs(newSum - oldSum)/((self.height/self.gridSize - 1)*(self.length/self.gridSize - 1))
                self.errorHistory.append(error)
                if error <= prec:
                    break
                
    sys = System(10,5,0.1)
    sys.boundaryInit(100,200,200,100)
    sys.solve(0.001,1.2)
    
    sys.plot("solution12.png")
    sys.plotConvergence("error.png")
    print sys.it

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

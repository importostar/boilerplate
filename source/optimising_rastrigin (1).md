---
title: optimising_rastrigin (1)
date: 2020-05-07
---
Example Python program optimising_rastrigin (1).py

## Modules

* import numpy as np
* import matplotlib.pyplot as plt
* from matplotlib import animation, rc

## Methods

* def plot(surface, positions, best_fitness, best_position, iteration):
* def run(iteration):

## Code

Python example

    # Imports
    import numpy as np
    import matplotlib.pyplot as plt
    from matplotlib import animation, rc
    
    
    # A way of plotting each step of the optimisation process.
    def plot(surface, positions, best_fitness, best_position, iteration):
        plt.cla()
        
        # Plot the feature / error surface.
        plt.pcolormesh(surface[0], surface[1], surface[2])
    
        # Plot all of the genepool.
        x, y = zip(*positions)
        plt.scatter(x, y, 1, 'k', edgecolors='face')
        
        # Plot the best gene.
        plt.scatter(best_position[0], best_position[1], 20, 'w', edgecolors='face')
    
        # Add the title to the plot.
        title = "iteration {}, fitness {}".format(iteration, best_fitness)
        plt.title(title)
    
        
    # Each time this function is ran, the optimisation process is furthered a step.
    def run(iteration):
      
        # Get the rastrigin error surface.
        surface = function.get_surface()
        
        # Get the gene pool.
        positions = ga.get_solutions()
        
        # Evaluate the fitnesses on the rastrigin surface
        fitnesses = [function.evaluate(pos) for pos in positions]
        
        # Inform the GA of the genepool's performance
        ga.set_fitnesses(fitnesses)
        
        # Get the best gene
        best_position, best_fitness = ga.get_best()
    
        # Plot the optimsation
        plot(surface, positions, best_fitness, best_position, iteration)
    
    
    # Genetic Algorithm parameters 
    elitism = 0.1
    population_size = 500
    mutation_rate = 0.8
    mutation_sigma = 0.1
    mutation_decay = 0.999
    mutation_limit = 0.01
    amount_optimisation_steps = 250
    dna_bounds = (-5.11, 5.11)
    dna_start_position = [4.8, 4.8]
    
    # Construct the test function
    function = Rastrigin()
    
    # Construct the GA
    ga = GA(len(dna_start_position),
            dna_bounds,
            dna_start_position,
            elitism,
            population_size,
            mutation_rate,
            mutation_sigma,
            mutation_decay,
            mutation_limit)
    
    # Create the matplotlib figure
    fig = plt.figure(figsize=(10, 10))
    
    # See this on making gifs with matplotlib:
    # https://matplotlib.org/api/animation_api.html
    anim = animation.FuncAnimation(fig, run, frames=amount_optimisation_steps)
    anim.save('rastrigin3_ga.mp4', fps=15)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

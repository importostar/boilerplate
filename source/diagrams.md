---
title: diagrams
date: 2020-05-07
---
Example Python program diagrams.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* from __future__ import division
* import cmath
* import utilities

## Methods

* def find_product(nums):
* def find_product_proof(n, r):
* def plot_diagonals(plot, nums):
* def draw_basic_complex_plane():
* def draw_de_moivre_3():
* def draw_diagonal_lines_3_to_10():
* def draw_3_when_theta_is_i():
* def draw_when_theta_is_i():
* def test_product_of_diagonals():
* def test_increasing_n():
* def test_when_theta_is_i():
* def test_varying_n_r_and_theta():
* def test_increasing_radius():
* def graphs():
* def tests():

## Code

Python example

    #!/usr/bin/env python
    '''
    Contains code to generate the graphs and data used in this IA
    '''
    
    
    from __future__ import division
    
    import cmath
    import utilities
    
    
    # Convenience functions
    
    def find_product(nums):
        '''Finds the product of the diagonals by manually finding and 
        multiplying the distance between roots. Assumes that the first
        root in the list is the radiating point.'''
        product = 1
        for vertex in nums[1:]:
            product *= utilities.find_distance(nums[0], vertex)
        return product
        
    def find_product_proof(n, r):
        '''Finds the product based on the general equation derived in 
        the paper.'''
        return n * r**((n - 1)/n)
        
    def plot_diagonals(plot, nums):
        '''Given a plot, draws red lines to indicate the diagonals.
        Assumes that the first root in the list is the radiating point.'''
        for vertex in nums:
            plot.add_line(nums[0], vertex, color='red')
                
    
    # Graphs
        
    def draw_basic_complex_plane():
        '''Draws a basic complex plane used in the first section of this
        paper. (figure 1.1)'''
        plot = utilities.Plot((-1.2, 1.2), (-1.2, 1.2), 1, 1, figsize=(4, 4))
        point = utilities.S(0.5 + utilities.sympy.sin(utilities.sympy.pi/3)*1j)
        
        plot.add_points([point])
        plot.add_circle(1)
        
        plot.add_line(0, point)
        plot.add_line(0, utilities.S(0.5), color='blue')
        plot.add_line(utilities.S(0.5), point, color='blue')
        
        plot.add_annotation(r'$\theta$', (0.09, 0.03), color="purple")
        plot.add_annotation('$r$', (0.18, 0.42), color="red")
        plot.add_annotation('$a + bi$', (0.55, 0.85))
        
        plot.add_annotation(r'$a = r \cdot \cos{(\theta)}$', 
            (0.15, -0.15), color="blue")
        plot.add_annotation(r'$b = r \cdot \sin{(\theta)}i$', 
            (0.55, 0.35), color="blue")
        
        utilities.save(utilities.render(plot), 'basic-complex-plane')
        
    def draw_de_moivre_3():
        '''Creates figure 2.1 a and b'''
        nums = utilities.de_moivre(3, 1, 0)
        p1 = utilities.Plot((-1.2, 1.2), (-1.2, 1.2), 0.5, 0.5, figsize=(5, 5))
        p1.add_points(nums)
        p1.add_circle(1)
        utilities.save(utilities.render(p1), 'de_moivre_3-simple')
        
        p2 = p1.copy()
        plot_diagonals(p2, nums)
        av1 = (nums[0] + nums[1]) * 3 / 2
        av2 = (nums[0] + nums[2]) * 3 / 2
        d1 = float(utilities.find_distance(nums[0], nums[1]))
        d2 = float(utilities.find_distance(nums[0], nums[2]))
        p2.add_annotation(r'$distance \approx {0:.4f}$'.format(d1), (0.1, 0.6))
        p2.add_annotation(r'$distance \approx {0:.4f}$'.format(d2), (0.1, -0.6))
        utilities.save(utilities.render(p2), 'de_moivre_3-lines')
        
    def draw_diagonal_lines_3_to_10():
        '''Draws graphs for z^n - 1 = 0 with diagonals.'''
        for n in xrange(3, 11):
            nums = utilities.de_moivre(n, 1, 0)
            
            plot = utilities.Plot((-1.2, 1.2), (-1.2, 1.2), 1, 1, figsize=(3, 3))
            plot.add_points(nums)
            plot.add_circle(1)
            plot_diagonals(plot, nums)
            for index, vertex in enumerate(nums):
                plot.add_annotation('$z_{0}$'.format(index), 
                    utilities.tup(vertex), offset=(5, 5))
                
            utilities.save(utilities.render(plot), 'de_moivre_{0}'.format(n))
            
    def draw_3_when_theta_is_i():
        '''Draws roots and lines when z^3 - i = 0'''
        nums = utilities.de_moivre(3, 1, utilities.sympy.pi / 2)
        plot = utilities.Plot((-1.2, 1.2), (-1.2, 1.2), 1, 1, figsize=(5, 5))
        plot.add_points(nums)
        plot.add_circle(1)
        utilities.save(utilities.render(plot), 'de_moivre_3_i-simple')
        
        plot2 = plot.copy()
        plot_diagonals(plot2, nums)
        av1 = (nums[0] + nums[1]) * 3 / 2
        av2 = (nums[0] + nums[2]) * 3 / 2
        d1 = float(utilities.find_distance(nums[0], nums[1]))
        d2 = float(utilities.find_distance(nums[0], nums[2]))
        plot2.add_annotation(r'$distance \approx {0:.4f}$'.format(d1), (0.1, 0.55))
        plot2.add_annotation(r'$distance \approx {0:.4f}$'.format(d2), (0.4, -0.5))
        utilities.save(utilities.render(plot2), 'de_moivre_3_i-lines')
            
    def draw_when_theta_is_i():
        '''Draws multiple graphs when z^n - 1 = 0'''
        for n in xrange(3, 6):
            nums = utilities.de_moivre(n, 1, utilities.sympy.pi / 2)
            plot = utilities.Plot((-1.2, 1.2), (-1.2, 1.2), 1, 1, figsize=(5, 5))
            plot.add_points(nums)
            plot.add_circle(1)
            plot_diagonals(plot, nums)
            utilities.save(utilities.render(plot), 'de_moivre_{0}_i'.format(n))
        
        
    # Tests
        
    def test_product_of_diagonals():
        '''Tests that the product of the diagonals equals n for a small amount of n'''
        for n in xrange(3, 11):
            nums = utilities.de_moivre(n, 1, 0)
            
            print 'n =', n
            for vertex in nums:
                re, im = utilities.tup(vertex)
                print '   ', float(re), ',', float(im)
            print '   product = ', float(find_product(nums))
            for i in xrange(n):
                print '   @', r'(z - \cis{{\frac{{2\pi \cdot {0}}}{{{1}}})'.format(i, n)
            for vertex in nums:
                print '   >', float(utilities.find_distance(nums[0], vertex))
                
    def test_increasing_n():
        '''Tests the effects of increasing n from 3 to 1000 given z^n - 1 = 0'''
        for n in xrange(3, 1000):
            nums = utilities.de_moivre(n, 1, 0)
            prod = 1
            for vertex in nums[1:]:
                prod *= utilities.find_distance(nums[0], vertex)
            a = utilities.R(n)
            b = prod.evalf(10)
            if a != b:
                print a, b
        
    def test_when_theta_is_i():
        '''Determines what happens when z^n - i = 0'''
        for n in xrange(3, 6):
            nums = utilities.de_moivre(n, 1, utilities.sympy.pi / 2)
            
            print 'n = {0}'.format(n)
            print '    prod = ', find_product(nums).evalf(10)
            for num in nums:
                print '   >', num
            for num in nums:
                print '   @', num.evalf(4)
            for num in nums:
                print '   ?', utilities.find_distance(nums[0], num).evalf(5)
            
    def test_varying_n_r_and_theta():
        '''Determines what happens when n, r, and theta are varied, and
        if the general equation works.'''
        for n in xrange(3, 5):
            for r in xrange(1, 3):
                for theta in xrange(0, 8):
                    theta = utilities.sympy.pi * theta / 4
                    nums = utilities.de_moivre(n, r, theta)
                    direct_product = find_product(nums)
                    proof_product = utilities.S(find_product_proof(n, r))
                    
                    print '{0}: {1}: {2}'.format(n, r, theta)
                    print '   ', direct_product.evalf(8)
                    print '   ', proof_product.evalf(8)
    
    def test_increasing_radius():
        '''Tests the effects of increasing the radius.'''
        plot = utilities.Plot((-2, 2), (-2, 2), 0.5, 0.5, figsize=(8, 8))
        for r in xrange(1, 10):
            nums = utilities.de_moivre(4, r, 0)
            
            prod = find_product(nums)
            print r, prod, prod.evalf(10)
            print find_product_proof(4, r)
            
            plot.add_points(nums)
            plot.add_circle(r)
        #utilities.render(plot).show()
            
        
        
    def graphs():
        draw_basic_complex_plane()
        draw_de_moivre_3()
        draw_diagonal_lines_3_to_10()
        draw_3_when_theta_is_i()
        draw_when_theta_is_i()
        
    def tests():
        test_product_of_diagonals()
        test_increasing_n()
        test_when_theta_is_i()
        test_varying_n_r_and_theta()
        test_increasing_radius()
        
    if __name__ == '__main__':
        utilities.setup()
        graphs()
        tests()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

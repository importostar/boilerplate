---
title: SecretColorsExample
date: 2020-05-07
---
Example Python program SecretColorsExample.py

## Modules

* import matplotlib
* import matplotlib.pylab as plt
* import numpy as np
* from SecretColors.palette import Palette

## Methods

* def test_scatter():
* def test_bar():
* def test_bar2():
* def test_lines():
* def test_heatmap():
* def test_distribution():

## Code

Python example

    """
    Rohit Suratekar
    September 2018
    Examples of newly developed library SecretColors
    https://pypi.org/project/SecretColors/
    """
    import matplotlib
    import matplotlib.pylab as plt
    import numpy as np
    
    from SecretColors.palette import Palette
    
    ibm = Palette("ibm")
    
    
    def test_scatter():
        x_data = np.random.randint(0, 100, 300)
        y_data = np.random.randint(0, 100, 300)
        z_data = np.random.randint(0, 100, 300)
        plt.figure(figsize=(9, 6))
    
        plt.subplot(131)
        plt.scatter(x_data, y_data, c=z_data, cmap="Blues")
        plt.title('Default')
        plt.colorbar()
        plt.subplot(132)
        plt.title('SecretColors (default)')
        plt.scatter(x_data, y_data, c=z_data, cmap=ibm.cmap_of(matplotlib,
                                                               ibm.cerulean()))
    
        plt.colorbar()
    
        plt.subplot(133)
        plt.scatter(x_data, y_data, c=z_data, cmap=ibm.cmap_of(matplotlib,
                                                               ibm.cerulean(),
                                                               start_grade=30))
        plt.title('SecretColors (graded)')
        plt.colorbar()
        plt.show()
    
    
    def test_bar():
        x_data = np.random.random(8)
        ind = range(len(x_data))
        labels = ['data_' + str(x) for x in ind]
        plt.figure(figsize=(9, 6))
    
        cmap = matplotlib.cm.get_cmap('Reds')
        plt.subplot(121)
        colors = [cmap(x) for x in x_data]
        plt.bar(ind, x_data, color=colors)
        plt.xticks(ind, labels, rotation=90)
        plt.title("Default")
    
        plt.subplot(122)
        new_colors = ibm.normalized_colors_for(
            matplotlib, x_data, ibm.red(), upper_bound=1.2)
        plt.bar(ind, x_data, color=new_colors)
        plt.xticks(ind, labels, rotation=90)
        plt.title("SecretColors")
    
        plt.show()
    
    
    def test_bar2():
        x_data = np.random.random(10)
        ind = range(len(x_data))
        labels = ['data_' + str(x) for x in ind]
        plt.figure(figsize=(9, 6))
    
        plt.subplot(121)
        for i in ind:
            plt.bar(i, x_data[i])
        plt.xticks(ind, labels, rotation=90)
        plt.title("Default")
    
        plt.subplot(122)
        for i in ind:
            plt.bar(i, x_data[i], color=ibm.base(x_data)[i])
        plt.xticks(ind, labels, rotation=90)
        plt.title("SecretColors")
    
        plt.show()
    
    
    def test_lines():
        all_data = []
        for d in range(4):
            data = np.random.random(30) + d * 0.8
            all_data.append(data)
        time = range(len(all_data[0]))
        plt.figure(figsize=(9, 6))
    
        plt.subplot(121)
        colors = ["r", "g", "b", "y"]
        i = 0
        for data in all_data:
            plt.plot(time, data, linewidth=4, color=colors[i])
            i += 1
        plt.title("Default")
    
        plt.subplot(122)
        new_colors = [ibm.red(), ibm.green(), ibm.blue(), ibm.yellow()]
        i = 0
        for data in all_data:
            plt.plot(time, data, linewidth=4, color=new_colors[i])
            i += 1
        plt.title("SecretColors")
    
        plt.show()
    
    
    def test_heatmap():
        a = np.random.random((16, 16))
    
        plt.subplot(121)
        plt.imshow(a, cmap='Greens', interpolation='nearest')
    
        plt.subplot(122)
        plt.imshow(a, cmap=ibm.cmap_of(matplotlib, ibm.green()),
                   interpolation='nearest')
    
        plt.show()
    
    
    def test_distribution():
        mu, sigma = 100, 15
        mu2, sigma2 = 150, 20
        x = mu + sigma * np.random.randn(10000)
        y = mu2 + sigma2 * np.random.randn(10000)
    
        plt.subplot(121)
        plt.hist(x, 30, alpha=0.8)
        plt.hist(y, 30, alpha=0.8)
    
        plt.subplot(122)
        plt.hist(x, 30, alpha=0.8, color=ibm.cerulean())
        plt.hist(y, 30, alpha=0.8, color=ibm.orange())
    
        plt.show()
    
    
    if __name__ == "__main__":
        test_scatter()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: timeseries_plot_using_matplotlib
date: 2020-05-07
---
Example Python program timeseries_plot_using_matplotlib.py

## Modules

* import pandas as pd
* import matplotlib
* import matplotlib.cm as cm
* from matplotlib import pyplot as plt
* from matplotlib import dates as mdates
* import seaborn as sns
* import click

## Methods

* def scatterplot(input, output):
* def cli(input, output):

## Code

Python example

    # -*- coding: utf-8 -*-
    """visualizer: basic visualization module for debugging
    """
    
    import pandas as pd
    import matplotlib
    import matplotlib.cm as cm
    from matplotlib import pyplot as plt
    from matplotlib import dates as mdates
    import seaborn as sns
    import click
    
    
    def scatterplot(input, output):
        click.echo('Start processing of visualization')
    
        click.echo('Loading CSV file {}'.format(input))
        # Load N-Detection formatted CSV file
        df = pd.read_csv(input)
    
        # Convert date-string columns to datetime object
        df['TIME'] = pd.to_datetime(df['TIME'])
    
        # Setting plotting styles
        sns.set()
        sns.set_style("darkgrid")
        sns.set(font='Tahoma', font_scale=1.4)
        c = sns.color_palette("Set2", 10)
    
        f, ax = plt.subplots(figsize=(20, 10))
        for i, (n, g) in enumerate(df.groupby('GROUP')):
            plt.plot(g['TIME'], g['Y'], 'o', label=n, color=c[i % 10])
    
        ax.set_ylim(0, ax.get_ylim()[1] * 1.2)
        ax.set_ylabel('Y Axis label')
        ax.legend(loc="upper left", bbox_to_anchor=(1, 1))
        date_formatter = mdates.DateFormatter('%Y%m%d %H:%M')
        ax.xaxis.set_major_formatter(date_formatter)
        f.autofmt_xdate()
    
        # Output as PNG file
        f.savefig(output, bbox_inches='tight')
    
        click.echo('Write scatter-plot as {}'.format(output))
        return None
    
    
    @click.command()
    @click.option('--input', default=None, help='Path of CSV file to process')
    @click.option('--output', default='scatterplot.png', help='Path to output file')
    def cli(input, output):
        scatterplot(input, output)
    
    
    if __name__ == '__main__':
        cli()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

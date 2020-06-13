---
title: geopandas_example
date: 2020-05-07
---
Example Python program geopandas_example.py

## Modules

* import matplotlib.pyplot as pl
* import geopandas as gpd

## Code

Python example

    """
    Getting started with Geo Pandas.
    
    This gist quickly shows how to create a world's heatmap with Python.
    """
    # Import matplotlib. Figure can be done by just using geopandas library
    import matplotlib.pyplot as pl
    # Import geopandas
    import geopandas as gpd
    # Load countries polygons
    world = gpd.read_file(gpd.datasets.get_path('naturalearth_lowres'))
    # Load cities polygons
    cities = gpd.read_file(gpd.datasets.get_path('naturalearth_cities'))
    # Create matplotlib figure-related objects
    fig, ax = pl.subplots(1, figsize=(10, 6))
    # invokes geopandas dataframe PLOT method
    # Last parameter binds method with matplotlib object
    world.plot(column='gdp_md_est', edgecolor='#555555', ax=ax)
    # Disables axis
    pl.axis('off')
    # Reduce black spaces on margins
    pl.tight_layout()
    # Save figure in current directory
    fig.savefig('example.pdf')

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: config_example
date: 2020-05-07
---
Example Python program config_example.py

## Modules

* import json
* import argparse
* import numpy as np
* import matplotlib
* import matplotlib.pyplot as plt

## Methods

* def main(args):

## Code

Python example

    import json
    import argparse
    
    import numpy as np
    import matplotlib
    import matplotlib.pyplot as plt
    
    matplotlib.rcParams['text.usetex'] = True
    
    # Inspiration came from https://stackoverflow.com/q/3609852/8931942
    
    
    def main(args):
        # Example taken from matplotlib docs
        # https://matplotlib.org/2.0.2/examples/lines_bars_and_markers/fill_demo.html
        x = np.linspace(0, 1, 500)
        y = np.sin(4 * np.pi * x) * np.exp(-5 * x)
    
        fig, ax = plt.subplots()
    
        ax.fill(x, y, zorder=10)
        ax.grid(True, zorder=5)
    
        if hasattr(args, 'plot_title'):
            plt.title(args.plot_title)
        if hasattr(args, 'x_axis_title'):
            plt.xlabel(args.x_axis_title)
        if hasattr(args, 'y_axis_title'):
            plt.ylabel(args.y_axis_title)
    
        if hasattr(args, 'plot_name'):
            # extensions = ['.pdf', '.png', '.svg', '.jpg']
            # writing SVG is slow
            extensions = ['.pdf', '.png', '.jpg']
            for extension in extensions:
                plt.savefig(args.plot_name + extension)
    
    
    if __name__ == '__main__':
        cli_parser = argparse.ArgumentParser(
            description='configuration arguments provided at run time from the CLI'
        )
        cli_parser.add_argument(
            '-c',
            '--config_file',
            dest='config_file',
            type=str,
            default=None,
            help='config file',
        )
        cli_parser.add_argument(
            '-x',
            '--x_axis_title',
            dest='x_axis_title',
            type=str,
            default='',
            help='x-axis name',
        )
    
        args, unknown = cli_parser.parse_known_args()
    
        parser = argparse.ArgumentParser(parents=[cli_parser], add_help=False)
    
        if args.config_file is not None:
            if '.json' in args.config_file:
                # The escaping of "\t" in the config file is necesarry as
                # otherwise Python will try to treat is as the string escape
                # sequence for ASCII Horizontal Tab when it encounters it
                # during json.load
                config = json.load(open(args.config_file))
                parser.set_defaults(**config)
    
                [
                    parser.add_argument(arg)
                    for arg in [arg for arg in unknown if arg.startswith('--')]
                    if arg.split('--')[-1] in config
                ]
    
        args = parser.parse_args()
    
        main(args)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: visualize
date: 2020-05-07
---
Example Python program visualize.py


## Methods

* def get_fontproperties(font, fontsize):
* def apply_style(ax, font='times', fontsize=8, linewidth=1.0,
* def inch(cm):
* def golden_ratio(value):
* def cdf(X, ax, kwargs=dict()):
* def one_minus_cdf(ax):
* def get_index(n, ncols=4):
* def get_plots(n, ncols=4, figsize=None, width=3, height=2):
* def get_color_map(cmap, n):
* def get_color(colormap, n, i):
* def get_line_style(i, styles=['o-', 'v-', 's-', '+:', 'x:', 'D:'], marker_edge_colors=['k', 'k', 'k', None, None, 'k']):
* def get_flat_arrays(*args):
* def correlation(X, Y):
* def draw_scatter(ax, X, Y, do_sampling=False, n=100000, show_polyfit=False):
* def draw_violin(ax, factor, returns, do_sampling=False, n=100000):
* def draw_bar(ax, factor, returns, do_sampling=False, n=100000):
* def draw_corr(ax, factor, returns, period=120):

## Code

Python example

    def get_fontproperties(font, fontsize):
        if font == 'monaco':
            fontproperties = mpl.font_manager.FontProperties(fname='Fonts/Monaco.ttf', size=fontsize)
        elif font == 'times':
            fontproperties = mpl.font_manager.FontProperties(fname='Fonts/Times New Roman.ttf', size=fontsize)
        elif font == 'helvetica':
            fontproperties = mpl.font_manager.FontProperties(fname='Fonts/Helvetica.ttf', size=fontsize)
        elif font == 'libertine':
            fontproperties = mpl.font_manager.FontProperties(fname='Fonts/Libertine.ttf', size=fontsize)
        elif font == 'nanum_gothic':
            fontproperties = mpl.font_manager.FontProperties(fname='Fonts/NanumGothic.ttf', size=fontsize)
        elif font == 'nanum_myeongjo':
            fontproperties = mpl.font_manager.FontProperties(fname='Fonts/NanumMyeongjo.ttf', size=fontsize)
        else:
            raise AssertionError('The fontprop {} is not supported.'.format(font))
    
        return fontproperties
    
    def apply_style(ax, font='times', fontsize=8, linewidth=1.0,
                    title=None, xlabel=None, ylabel=None,
                    xscale=None, yscale=None, basex=None, basey=None,
                    ytick_rotation=0, xtick_rotation=0,
                    xtick_frequency=None, ytick_frequency=None,
                    show_grid=True, show_legend=False, legend_font_size=None,
                    xaxis_formatter=None, yaxis_formatter=None,
                    xlim=None, ylim=None, xticks=None, yticks=None,
                    xtick_horizontal_alignment='center',
                    ytick_horizontal_alignment='right'):
        
        fontproperties = get_fontproperties(font, fontsize)
        
        if title is not None:
            ax.set_title('{}'.format(title), fontproperties=fontproperties)
        if xlabel is not None:
            ax.set_xlabel('{}'.format(xlabel), fontproperties=fontproperties)
        if ylabel is not None:
            ax.set_ylabel('{}'.format(ylabel), fontproperties=fontproperties)
    
        if xtick_frequency is not None:
            loc = mpl.ticker.MultipleLocator(base=xtick_frequency)
            ax.get_xaxis().set_major_locator(loc)
        if ytick_frequency is not None:
            loc = mpl.ticker.MultipleLocator(base=ytick_frequency)
            ax.get_yaxis().set_major_locator(loc)
    
        for tick in ax.get_yticklabels():
            tick.set_fontproperties(fontproperties)
            tick.set_rotation(ytick_rotation)
            tick.set_horizontalalignment(ytick_horizontal_alignment)
        for tick in ax.get_xticklabels():
            tick.set_fontproperties(fontproperties)
            tick.set_rotation(xtick_rotation)
            tick.set_horizontalalignment(xtick_horizontal_alignment)
    
        ax.get_xaxis().set_tick_params(width=linewidth)
        ax.get_yaxis().set_tick_params(width=linewidth)
    
        for axis in ['top','bottom','left','right']:
            ax.spines[axis].set_linewidth(linewidth)
    
        if xaxis_formatter is not None:
            ax.get_xaxis().set_major_formatter(xaxis_formatter)
        if yaxis_formatter is not None:
            ax.get_yaxis().set_major_formatter(yaxis_formatter)
    
        if show_grid:
            ax.set_axisbelow(True)
            ax.grid(True, linestyle=':', linewidth=linewidth*0.6, color='silver')
    
        if xscale is not None:
            if basex is not None:
                ax.set_xscale(xscale, basex=basex)
            else:
                ax.set_xscale(xscale)
        if yscale is not None:
            if basey is not None:
                ax.set_yscale(yscale, basey=basey)
            else:
                ax.set_yscale(yscale)
    
        if xlim is not None:
            ax.set_xlim(xlim)
        if ylim is not None:
            ax.set_ylim(ylim)
        
        if xticks is not None:
            ax.set_xticks(xticks)
        if yticks is not None:
            ax.set_yticks(yticks)
    
        if show_legend:
            if title is not None and 'CDF' in title:
                loc = 'lower right'
            else:
                loc = 'best'
            if legend_font_size is None:
                legend_font_size = fontsize - 1
            legend = ax.legend(
                    loc=loc, prop=get_fontproperties(font, legend_font_size), edgecolor='k', labelspacing=0.5,
                    borderpad=0.5)
            legend.get_frame().set_linewidth(linewidth)
    
    def inch(cm):
        return cm * 0.393701
    
    def golden_ratio(value):
        return value / 1.61803398875
    
    def cdf(X, ax, kwargs=dict()):
        n = np.arange(1, len(X) + 1) / np.float(len(X))
        Xs = np.sort(X)
        ax.step(Xs, n, **kwargs)
    
    def one_minus_cdf(ax):
        for line in ax.lines:
            line.set_ydata([1-v for v in line.get_ydata()])
    
    def get_index(n, ncols=4):
        nrows = math.ceil(n / ncols)
        indexes = []
        count = 0
        for i in range(nrows):
            for j in range(ncols):
                indexes.append((i, j))
                count += 1
                if count == n:
                    break
        return indexes
    
    def get_plots(n, ncols=4, figsize=None, width=3, height=2):
        nrows = math.ceil(n / ncols)
        if figsize is None:
            figsize = (width * ncols, height * nrows)
        fig, axes = plt.subplots(ncols=ncols, nrows=nrows, figsize=figsize)
        
        return fig, axes
    
    def get_color_map(cmap, n):
        cmap = plt.cm.get_cmap(cmap)
        norm = mpl.colors.Normalize(vmin=0, vmax=n-1)
        return cmap, norm
    
    def get_color(colormap, n, i):
        cmap = plt.cm.get_cmap(colormap)
        
        if colormap == 'Pastel1':
            n = 9
        elif colormap == 'Pastel2':
            n = 8
        elif colormap == 'Paired':
            n = 12
        elif colormap == 'Accent':
            n = 8
        elif colormap == 'Dark2':
            n = 8
        elif colormap == 'Set1':
            n = 9
        elif colormap == 'Set2':
            n = 8
        elif colormap == 'Set3':
            n = 12
        elif colormap == 'tab10':
            n = 10
        elif colormap == 'tab20':
            n = 20
            i = ((i * 2) % 20) + int(i / 10)
        elif colormap == 'tab20b':
            n = 20
            i = ((i * 4) % 20) + int(i / 5)
        elif colormap == 'tab20c':
            n = 20
            i = ((i * 4) % 20) + int(i / 5)
        else:
            n -= 1
        norm = mpl.colors.Normalize(vmin=0, vmax=n)
        return cmap(norm(i))
    
    def get_line_style(i, styles=['o-', 'v-', 's-', '+:', 'x:', 'D:'], marker_edge_colors=['k', 'k', 'k', None, None, 'k']):
        '''
        more line styles
        styles = [':', '-.', '--', '-']
        https://matplotlib.org/3.1.0/gallery/lines_bars_and_markers/linestyles.html
        https://matplotlib.org/3.1.0/gallery/lines_bars_and_markers/marker_reference.html
        https://matplotlib.org/2.0.2/api/markers_api.html
        https://matplotlib.org/3.1.1/gallery/lines_bars_and_markers/marker_fillstyle_reference.html
        '''
        return dict(style=styles[i], edge_color=marker_edge_colors[i])
    
    def get_flat_arrays(*args):
        flat = []
        for arr in args:
            flat.append(np.ndarray.flatten(arr))
        nans = np.isnan(flat[0])
        for arr in flat[1:]:
            nans += np.isnan(arr)
        for i in range(len(flat)):
            flat[i] = flat[i][~nans]
        return flat
    
    def correlation(X, Y):
        X = np.ndarray.flatten(X)
        Y = np.ndarray.flatten(Y)
        nans = np.isnan(X) + np.isnan(Y)
        X = X[~nans]
        Y = Y[~nans]
        return np.corrcoef(X, Y)[0][1]
    
    def draw_scatter(ax, X, Y, do_sampling=False, n=100000, show_polyfit=False):
        X, Y = get_flat_arrays(X, Y)
        if do_sampling:
            index = random.sample(range(X.size), n)
            X = X[index]
            Y = Y[index]
        
        ax.scatter(X, Y, marker=',', s=0.3, alpha=0.1)
        
        if show_polyfit:
            b, m = polyfit(X, Y, 1)
            ax.plot(X, b + m * X, '-', color='r', linewidth=1.0, alpha=0.5)
    
    def draw_violin(ax, factor, returns, do_sampling=False, n=100000):
        X, Y = get_flat_arrays(quantile(factor), returns)
        if do_sampling:
            index = random.sample(range(X.size), n)
            X = X[index]
            Y = Y[index]
        
        buckets = [[] for i in range(int(max(X)) + 1)]
        for x, y in zip(X, Y):
            buckets[int(x)].append(y)
        for i in range(len(buckets)):
            buckets[i] = 100 * (winsorize(np.array(buckets[i]), limits=(0.01, 0.01)) - 1)
    
        _ = ax.violinplot(
            buckets, range(len(buckets)), widths=0.9,
            showmeans=True, showextrema=True, showmedians=False)
    
    def draw_bar(ax, factor, returns, do_sampling=False, n=100000):
        X, Y = get_flat_arrays(quantile(factor), returns)
        if do_sampling:
            index = random.sample(range(X.size), n)
            X = X[index]
            Y = Y[index]
        
        buckets = [[] for i in range(int(max(X)) + 1)]
        for x, y in zip(X, Y):
            buckets[int(x)].append(y)
    
        geomean = []
        for bucket in buckets:
            geomean.append(100 * (gmean(bucket) - 1))
        ax.bar(list(range(int(max(X)) + 1)), geomean, edgecolor='k', linewidth=1.0)
    
    def draw_corr(ax, factor, returns, period=120):
        timestamps, values = [], []
        for i in range(len(returns)):
            if i < period:
                continue
            X = factor[i - period:i]
            Y = returns[i - period:i]
            X, Y = get_flat_arrays(X, Y)
            corr = correlation(X, Y)
            timestamps.append(pd.Timestamp(ITT[i]))
            values.append(corr)
        ax.plot(timestamps, values)
    
    abc = list('abcdefghijklnmopqrstuvwxyz')

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

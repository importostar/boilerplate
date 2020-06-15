---
title: bar
date: 2020-05-07
---
Example Python program bar.py

## Modules

* import numpy as np
* import matplotlib
* import matplotlib.pyplot as plt
* from matplotlib.patches import Ellipse

## Classes

* class Plot():

## Methods

* def __init__(self, data):
* def bar(self, xlim, ylim, bar_width, fill_color, x_title, y_title, filename=None):

## Code

Python example

    import numpy as np
    import matplotlib
    import matplotlib.pyplot as plt
    from matplotlib.patches import Ellipse
    
    '''
        现代风格的统计图
    '''
    class Plot():
    
        '''
            颜色表
        '''
        # 全局文字颜色
        TEXT_COLOR = np.array([80, 93, 111]) / 255
        # 网格线颜色
        GRID_COLOR = np.array([237, 240, 244]) / 255
        # 主色
        FILL_COLORS = {
            'PURPLE_1': np.array([130, 106, 249]) / 255,
            'PURPLE_2': np.array([158, 134, 255]) / 255,
            'PURPLE_3': np.array([208, 174, 255]) / 255,
            'PURPLE_4': np.array([247, 210, 255]) / 255,
            'BLUE_1'  : np.array([ 45, 153, 255]) / 255,
            'BLUE_2'  : np.array([131, 207, 255]) / 255,
            'BLUE_3'  : np.array([165, 243, 255]) / 255,
            'BLUE_4'  : np.array([204, 250, 255]) / 255,
            'GREEN_1' : np.array([ 44, 217, 197]) / 255,
            'GREEN_2' : np.array([ 96, 241, 200]) / 255,
            'GREEN_3' : np.array([164, 247, 204]) / 255,
            'GREEN_4' : np.array([192, 242, 220]) / 255,
            'YELLOW_1': np.array([255, 231,   0]) / 255,
            'YELLOW_2': np.array([255, 239,  90]) / 255,
            'YELLOW_3': np.array([255, 247, 174]) / 255,
            'YELLOW_4': np.array([255, 243, 214]) / 255,
            'RED_1'   : np.array([255, 108,  64]) / 255,
            'RED_2'   : np.array([255, 143, 109]) / 255,
            'RED_3'   : np.array([255, 189, 152]) / 255,
            'RED_4'   : np.array([255, 242, 212]) / 255
        }
    
        '''
            全局设置
        '''
        FONT_SIZE = 18
        CUSTOM_RC = {
            'text': {
                'color'       : TEXT_COLOR
            },
            'font': {
                'family'      : 'sans-serif',     # 使用非衬线字体
                'sans-serif'  : 'Arial',          # 定义非衬线字体
                'style'       : 'normal',         # 字体样式，可选 normal, italic, bold 等
                'weight'      : 'regular',        # 字重
            },
            'axes': {
                'labelcolor'  : TEXT_COLOR,       # 坐标轴标题的颜色
                'labelsize'   : FONT_SIZE,        # 坐标轴标题的字号
                'labelpad'    : 8.0,              # 坐标轴标题与刻度标签的距离
                'edgecolor'   : GRID_COLOR,       # 坐标轴边框的颜色
                'linewidth'   : 0.8,              # 坐标轴边框线的宽度
                'grid'        : True,             # 是否显示网格线
                'axisbelow'   : True,             # 网格线是否在最底层
            },
            'grid': {
                'color'       : GRID_COLOR,       # 网格线的颜色
                'linestyle'   : '-',              # 网格线样式
                'linewidth'   : 0.8,              # 网格线宽度
                'alpha'       : 1.0,              # 网格线透明度
            },
            'xtick': {
                'labelsize'   : FONT_SIZE,        # x 轴刻度标签字号
                'color'       : TEXT_COLOR,       # x 轴刻度标签颜色
                'major.size'  : 0,                # x 轴主刻度线那条短线的长度
                'minor.size'  : 0                 # x 轴副刻度线那条短线的长度
            },
            'ytick': {
                'labelsize'   : FONT_SIZE,        # y 轴刻度标签字号
                'color'       : TEXT_COLOR,       # y 轴刻度标签颜色
                'major.size'  : 0,                # y 轴主刻度线那条短线的长度
                'minor.size'  : 0                 # y 轴副刻度线那条短线的长度
            },
            'legend': {
                'fontsize'    : 14
            }
        }
    
        def __init__(self, data):
    
            self.data = data
    
            for name, settings in self.CUSTOM_RC.items():
                matplotlib.rc(name, **settings)
    
        '''
            条形图
        '''
        def bar(self, xlim, ylim, bar_width, fill_color, x_title, y_title, filename=None):
    
            origin_x = [p['x'] for p in self.data]
            # 将条形图往左移半格，目地是不让网格线穿过长条（美观）
            x = [(p['x'] - (origin_x[1] - origin_x[0]) / 2) for p in self.data]
            y = [p['y'] for p in self.data]
    
            # 图像尺寸
            fig, ax = plt.subplots(figsize=(8, 5))
            # x 轴和 y 轴的最大最小值
            ax.set_xlim(xlim)
            ax.set_ylim(ylim)
            # 计算 x 轴和 y 轴一个网格的长宽比，为了之后画圆形
            coor = ax.transData.transform([(xlim[0], xlim[0]), (xlim[1], ylim[1])])
            w = coor[1][0] - coor[0][0]
            h = coor[1][1] - coor[0][1]
            rate = (w / (xlim[1] - xlim[0])) / (h / (ylim[1] - ylim[0]))
    
            # 将 y 坐标向下移动一个圆的半径
            y = [(yi - bar_width * rate / 2.0) for yi in y]
    
            # 画条形图
            plt.bar(x=x,height=y, width=bar_width, color=self.FILL_COLORS[fill_color])
            # 画条形顶端的圆
            for xi, yi in zip(x, y):
                circle = Ellipse((xi, yi), width=bar_width, height=bar_width * rate, color=self.FILL_COLORS[fill_color], linewidth=0)
                ax.add_artist(circle)
    
            # 设置条形正下方的标签
            ax.set_xticks(x, minor=False)
            ax.set_xticklabels(origin_x, minor=False)
            # 设置条形两旁的网格线
            ax.set_xticks(origin_x, minor=True)
            ax.xaxis.grid(False, which='major')
            ax.xaxis.grid(True, which='minor')
    
            # 设置 x、y 轴的标题
            ax.set_xlabel(x_title)
            ax.set_ylabel(y_title)
    
            # 保存到文件
            if filename is not None:
                plt.savefig(filename, bbox_inches='tight', pad_inches=0)
    
    
    if __name__ == '__main__':
        data = [
            {'x': 1, 'y': 419},
            {'x': 2, 'y': 138},
            {'x': 3, 'y': 153},
            {'x': 4, 'y': 138},
            {'x': 5, 'y': 97},
            {'x': 6, 'y': 98},
            {'x': 7, 'y': 82},
            {'x': 8, 'y': 168},
            {'x': 9, 'y': 169}
        ]
        plot = Plot(data)
        plot.bar(
            xlim=(0, 9),
            ylim=(0, 500),
            bar_width=0.32,
            fill_color='PURPLE_3',
            x_title='Place ID',
            y_title='# of pedestrians',
            filename='1.pdf'
        )

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

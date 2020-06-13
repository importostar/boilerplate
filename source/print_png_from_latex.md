---
title: print_png_from_latex
date: 2020-05-07
---
Example Python program print_png_from_latex.py
This program creates a PyQt GUI

## Modules

* import os
* import sys
* from functools import partial
* import matplotlib
* import matplotlib.pyplot as plt
* from matplotlib.pyplot import figure
* from PySide import QtGui

## Methods

* def main():
* def generate_latex():

## Code

Python example

    import os
    import sys
    from functools import partial
    import matplotlib
    matplotlib.use('Qt4Agg')
    matplotlib.rcParams['backend.qt4'] = 'PySide'
    import matplotlib.pyplot as plt
    from matplotlib.pyplot import figure
    from PySide import QtGui
    
    # noinspection PyArgumentList
    
    
    def main():
        app = QtGui.QApplication.instance()  # checks if QApplication already exists
        if not app:  # create QApplication if it doesnt exist
            app = QtGui.QApplication(sys.argv)
        main_form = QtGui.QWidget()
        open_button = QtGui.QPushButton(parent=main_form)
        open_button.clicked.connect(partial(generate_latex))
        open_button.setText('LaTex to png')
        open_button.setIcon(QtGui.QIcon('glyphicons-145-folder-open.png'))
        main_form.show()
        main_form.adjustSize()
        sys.exit(app.exec_())
    
    
    def generate_latex():
        file_name, ext = QtGui.QFileDialog.getOpenFileName(
            parent=None,
            caption='open', directory='.',
            filter='Text description of LaTeX (*.txt)')
        if os.path.exists(file_name):
            with open(file_name) as f:
                data = f.read()
            tex_to_add = r"$" + data + r"$"
            fig = figure(figsize=(1, 1))
            ax = fig.add_axes([0, 0, 1, 1], frameon=False)
            ax.set_axis_off()
            # add text
            plt.text(0, 0, tex_to_add, fontsize=60)
            # save
            plt.savefig(
                os.path.splitext(
                    os.path.basename(file_name))[0] +
                '.png',
                bbox_inches='tight',
                transparent=True,
                frameon=False,
                edgecolor=None)
            # show
            plt.show()
    
    if __name__ == '__main__':
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: game (1)
date: 2020-05-07
---
Example Python program game (1).py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import time
* import math
* import sys
* from random import choice
* from PyQt5 import QtWidgets, QtCore
* from PyQt4 import QtGui as QtWidgets, QtCore

## Methods

* def show(board):
* def round(board):
* def shake(board, direction, max=2048):
* def shake_row(row, max=2048):
* def all_indices(haystack, needle):
* def cli():
* def main():
* def update():
* def key_press(event):

## Code

Example Python PyQt program :

    #!/usr/bin/env python3
    # vim: set ts=4 sts=0 et sw=4 smarttab :
    """2048 game in Python (cli, PyQt 4 or 5)."""
    
    import time
    import math
    import sys
    from random import choice
    
    ROW = 4
    
    def show(board):
        """Print the 2048 board."""
        print("")
        for i in range(0, len(board), ROW):
            print("".join(("{0:^5}".format(cell) for cell in board[i:i+ROW])))
        print("")
    
    
    def round(board):
        """
        Insert a 2 at a random available position (where a 0 sits).
    
        Return a new board.
        """
        index = choice(tuple(all_indices(board, 0)))
        return tuple(board[:index]) + (2,) + tuple(board[index+1:])
    
    
    def shake(board, direction, max=2048):
        """
        Shake the board in a given direction in wasd.
    
        Return a new board.
        """
        rows = [*board]
        direction = direction.lower()
        if direction not in 'wasd':
            raise ValueError("{} does nothing".format(direction))
    
        for i in range(ROW):
            if direction == 'a':
                start = i * ROW
                end = start + ROW
                rows[start:end] = shake_row(board[start:end], max)
    
            elif direction == 'd':
                start = i * ROW - 1
                end = start + ROW
                # -1 is the last element and not the one before the first one.
                # None must be used instead.
                if start == -1:
                    start = None
                rows[end:start:-1] = shake_row(board[end:start:-1], max)
    
            elif direction in 'w':
                rows[i::ROW] = shake_row(board[i::ROW], max)
    
            elif direction in 's':
                start = (ROW - 1) * ROW + i
                rows[start::-ROW] = shake_row(board[start::-ROW], max)
        return tuple(rows)
    
    
    def shake_row(row, max=2048):
        """
        Shake a given row towards its beginning.
    
        Return a new row.
        """
        l = len(row)
        row = [i for i in row if i != 0]
        m = 2
        while m < max:
            indices = tuple(all_indices(row, m))
            n = m*2
            for i in indices[:-1]:
                if row[i] == row[i+1] == m:
                    row[i] = n
                    row[i+1] = None
            row = [i for i in row if i is not None]
            m = n
    
        row.extend([0] * (l - len(row)))
        return tuple(row)
    
    
    def all_indices(haystack, needle):
        """Like list.index but for all the indices."""
        try:
            indice = -1
            while True:
                indice = haystack.index(needle, indice+1)
                yield indice
        except ValueError:
            pass
    
    
    def cli():
        """Play the CLI version of the game."""
        board = tuple([0] * ROW**2)
        board = round(round(board))
        s = "w"
        while s in "wasd":
            show(board)
            s = input("Shake the board with WASD: ").lower()
            board = shake(board, s)
            board = round(board)
    
    
    def main():
        """Play the Qt verson of the game."""
        app = QtWidgets.QApplication(sys.argv)
        window = QtWidgets.QWidget()
        grid = QtWidgets.QGridLayout()
        labels = []
        for i in range(ROW**2):
            label = QtWidgets.QLabel("0")
            label.setAlignment(QtCore.Qt.AlignCenter)
            labels.append(label)
            grid.addWidget(label, i // ROW, i % ROW)
        window.setLayout(grid)
    
        board = tuple([0] * ROW**2)
        board = round(round(board))
    
        keys = {
            QtCore.Qt.Key_Up: "w",
            QtCore.Qt.Key_Left: "a",
            QtCore.Qt.Key_Down: "s",
            QtCore.Qt.Key_Right: "d",
        }
    
        def update():
            """Update the state of the board."""
            for i, v in enumerate(board):
                labels[i].setText(str(v))
                x = math.log(max(1, v) / math.log(2))
                font_size = (1.5)**x + 20
                color = x / 10 * 360
                labels[i].setStyleSheet(
                    "font-size : {0:0.0f}px;"
                    "background-color : hsl({1:0.0f}, 100%, 50%);"
                    "min-width: 120px;"
                    "min-height: 120px;"
                    .format(font_size, color)
                )
            window.update()
    
        def key_press(event):
            """React to a pressed key by playing."""
            nonlocal board
    
            key = event.key()
            try:
                w = keys[key] if key in keys else chr(key).lower()
            except ValueError:
                print("Key unknown {}".format(key), file=sys.stderr)
                return
    
            try:
                m = 4
                while m < 2048:
                    new_board = shake(board, w, m)
                    if new_board != board:
                        board = new_board
                        time.sleep(.1)
                        update()
                        app.processEvents()
                    else:
                        board = new_board
                    m *= 2
                update()
                app.processEvents()
                time.sleep(.1)
                try:
                    board = round(board)
                except IndexError:
                    msg_box = QtWidgets.QMessageBox()
                    msg_box.setText("You've lost!")
                    msg_box.exec_()
                    board = tuple([0] * ROW**2)
                    board = round(round(board))
    
                update()
                app.processEvents()
            except ValueError:
                pass
    
        update()
    
        window.keyPressEvent = key_press
        window.show()
        app.exec_()
    
    
    if __name__ == "__main__":
        try:
            from PyQt5 import QtWidgets, QtCore
            main()
        except ImportError:
            try:
                from PyQt4 import QtGui as QtWidgets, QtCore
                main()
            except ImportError:
                print("Install PyQt to play a colorful version of 2048.",
                      "On Anaconda use: `conda install pyqt'\n"
    	              "Otherwise: `pip install pyqt5'\n",
                      file=sys.stderr)
                cli()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

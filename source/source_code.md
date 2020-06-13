---
title: source_code
date: 2020-05-07
---
Example Python program source_code.py
This program creates a PyQt GUI

## Modules

* import difflib
* import sys
* from pathlib import Path
* from PyQt5.QtWidgets import (QApplication,
* from PyQt5.QtGui import QIcon, QColor

## Classes

* class Window(QMainWindow):
* class MainWindow(Window):
* class DuplicateWindow(Window):
* class DiffWindow(Window):

## Methods

* def __init__(self):
* def initUI(self):
* def run(self):
* def autosave(self):
* def done_pressed(self):
* def __init__(self):
* def done_pressed(self, pressed):
* def __init__(self):
* def done_pressed(self):
* def __init__(self):

## Code

Example Python PyQt program :

    #Computer Graphics Project
    ''' Submitted by: Nimesh Babu Oli
                      PAS072BCT628
    '''
    import difflib
    import sys
    
    from pathlib import Path
    
    from PyQt5.QtWidgets import (QApplication,
                                QMainWindow,
                                QAction,
                                QPushButton,
                                QTextEdit,
                                QPlainTextEdit,
                                QGridLayout,
                                QComboBox,
                                QLabel,
                                QLineEdit,
                                QWidget,
                                QFrame,
                                qApp)
    from PyQt5.QtGui import QIcon, QColor
    
    ORIG_TEXT = 'initial.txt' # First file is saved here.
    DUPL_TEXT = 'final.txt' # second duplicate file is saved here.
    
    
    class Window(QMainWindow):
        def __init__(self):
            super().__init__()
            self.initUI()
    
        def initUI(self):
            self.done_button = QPushButton('भयो', self)
            self.done_button.move(140,300)
            self.done_button.clicked[bool].connect(self.done_pressed)
    
            self.setGeometry(450,300, 550, 350)
            self.setWindowTitle('Computer Graphics Project')
    
    
        def run(self):
            self.show()
    
        def autosave(self):
            file_path = Path(__file__)
            save_path = file_path
            with save_path.with_name(self.SAVE_LOC).open('w', encoding='utf8') as f:
                f.write(str(self.text_edit.toPlainText()))
    
        def done_pressed(self):
            pass
    
    
    class MainWindow(Window):
        def __init__(self):
            super().__init__()
            self.SAVE_LOC = ORIG_TEXT
    
            self.initUI()
    
            self.original_text_edit_lbl = QLabel('प्रथम अक्षर/वाक्य', self)
            self.original_text_edit_lbl.move(80, 70)
        
            self.original_text_edit= QPlainTextEdit(self)
            self.original_text_edit.setPlaceholderText("कृपया केहि लेख्नुहोस|")
            self.original_text_edit.setMinimumWidth(385)
            self.original_text_edit.move(50, 100)
            self.original_text_edit.setMinimumSize(300, 200)  # good if you want to insert this into a layout
    
            self.original_text_edit.textChanged.connect(self.autosave)
    
            self.text_edit = self.original_text_edit
    
            self.run()
    
        def done_pressed(self, pressed):
            self.original_text_edit.setDisabled(True)  # make text box uneditable
            self.done_button.setDisabled(True)  #disable this button
            self.statusBar().showMessage('          तपाईले अब यसमा केहि पनि लेख्न सक्नु हुन्न, कृपया बन्द गर्नुहोस्|')
    
            # show other window
            self.duplicate_window = DuplicateWindow()
            self.duplicate_window.show()
    
    
    class DuplicateWindow(Window):
        def __init__(self):
            super().__init__()
            self.SAVE_LOC = DUPL_TEXT # save text to DUPL_TEXT
    
            self.initUI()
    
            self.duplicate_text_edit_lbl = QLabel('दोस्रो सब्द/वाक्य', self)
            self.duplicate_text_edit_lbl.move(80, 70)
     
            self.duplicate_text_edit= QPlainTextEdit(self)
            self.duplicate_text_edit.setPlaceholderText("कृपया पहिलेको सब्द/वाक्यको नक्कल गर्नुहोस|")
            self.duplicate_text_edit.setMinimumWidth(385)
            self.duplicate_text_edit.move(50, 100)
            self.duplicate_text_edit.setMinimumSize(100, 200)
    
    
            self.duplicate_text_edit.textChanged.connect(self.autosave)
    
            self.text_edit = self.duplicate_text_edit
    
    
            self.run()
    
        def done_pressed(self):
            self.diff_window = DiffWindow()
            self.diff_window.show()
    
    
    class DiffWindow(Window):
        def __init__(self):
            super().__init__()
            super().initUI()
    
            # d = difflib.Differ()
            of = Path(__file__).with_name(ORIG_TEXT).open('r',encoding='utf8')
            df = Path(__file__).with_name(DUPL_TEXT).open('r',encoding='utf8')
    
            diff = difflib.unified_diff(of.read(), df.read(), lineterm='')
    
            self.diff_text_lbl = QLabel('दुई बीचको भेद:', self)
            self.diff_text_lbl.move(80, 70)
     
            self.diff_text= QTextEdit(self)
            self.diff_text.append('\n'.join(diff))
            self.diff_text.setMinimumWidth(385)
            self.diff_text.setMinimumSize(100, 200)  # good if you want to insert this into a layout
            self.diff_text.move(50, 100)
            self.diff_text.setReadOnly(True)
    
            self.setGeometry(300, 300, 550, 350)
    
            self.done_button.setDisabled(True)
    
    
            self.run()
    
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        main_window = MainWindow()
        main_window.show()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

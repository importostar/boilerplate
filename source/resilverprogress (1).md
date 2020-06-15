---
title: resilverprogress (1)
date: 2020-05-07
---
Example Python program resilverprogress (1).py
This program creates a PyQt GUI

## Modules

* import re, subprocess, sys
* from PyQt5.QtCore import Qt, QTimer
* from PyQt5.QtWidgets import (

## Methods

* def get_status(pool):
* def init_ui(pool):
* def update_status(pool):
* def start_timer(pool, interval=300000):
*   def handler():

## Code

Example Python PyQt program :

    #!/usr/bin/env python3
    
    import re, subprocess, sys
    
    from PyQt5.QtCore import Qt, QTimer
    from PyQt5.QtWidgets import (
      QApplication,
      QWidget,
      QLabel,
      QProgressBar,
      QHBoxLayout,
      QVBoxLayout,
    )
    
    percent_re = re.compile(r'([\d.]+)%')
    def get_status(pool):
      output = subprocess.check_output(['gksudo', 'zpool', 'status', pool],
                                       universal_newlines=True)
      prev = percent = percent_match = None
      for line in output.split('\n'):
        if '%' in line:
          percent_match = percent_re.search(line)
          break
        prev = line
      if percent_match is None:
        return None
    
      percent = float(percent_match.group(1))
    
      return prev.strip(), percent
    
    def init_ui(pool):
      # bit of a hack but it allows us to reload the module without a segfault
      global app, main_window, details_label, progress_bar
      try:
        app
      except NameError:
        app = QApplication(sys.argv)
      else:
        main_window.destroy()
      main_window = QWidget()
      main_window.resize(250, 150)
      main_window.move(300, 300)
      main_window.setWindowTitle('Resilver progress of {}'.format(pool))
      hbox = QHBoxLayout()
      # hbox.addStretch(1)
      vbox = QVBoxLayout()
      # vbox.addStretch(1)
      hbox.addLayout(vbox)
      main_window.setLayout(hbox)
      details_label = QLabel('loading…')
      details_label.setAlignment(Qt.AlignCenter)
      vbox.addWidget(details_label)
      progress_bar = QProgressBar()
      progress_bar.setAlignment(Qt.AlignCenter)
      vbox.addWidget(progress_bar)
    
    def update_status(pool):
      details, percent = get_status(pool)
      details_label.setText(details)
      progress_bar.setValue(percent)
      main_window.setWindowTitle('{}% — Resilver progress of {}'.format(percent, pool))
    
    def start_timer(pool, interval=300000):
      global timer
      timer = QTimer()
      timer.setInterval(interval)
      def handler():
        update_status(pool)
      timer.timeout.connect(handler)
      timer.start()
    
    if __name__ == '__main__':
      pool = sys.argv[1]
      init_ui(pool)
      main_window.show()
      update_status(pool)
      start_timer(pool)
      sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

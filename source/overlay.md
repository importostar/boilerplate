---
title: overlay
date: 2020-05-07
---
Example Python program overlay.py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtWidgets import QApplication, QWidget, QLabel, QGraphicsDropShadowEffect, QVBoxLayout, QHBoxLayout
* import sys
* from PyQt5.QtCore import Qt
* from PyQt5.QtGui import QColor, QPicture, QPainter, QPen

## Code

Example Python PyQt program :

    # https://stackoverflow.com/questions/51960766/python-text-overlay-on-top-of-everything-else#comment90884394_51960766
    # TODO This is not enough, perhaps https://github.com/AzoRAI/DX11OverlayExample will do it?
    from PyQt5.QtWidgets import QApplication, QWidget, QLabel, QGraphicsDropShadowEffect, QVBoxLayout, QHBoxLayout
    import sys
    from PyQt5.QtCore import Qt
    from PyQt5.QtGui import QColor, QPicture, QPainter, QPen
    
    app = QApplication(sys.argv) # Our application
    
    window = QWidget() # The window we'll be using.
    
    window.setAttribute(Qt.WA_TranslucentBackground, True) # Allows us to have a transparent window.
    window.setWindowFlags(Qt.SplashScreen | Qt.FramelessWindowHint | Qt.WindowStaysOnTopHint | Qt.WindowSystemMenuHint | Qt.CustomizeWindowHint)
    # Qt.SplashScreen identifies ourselves as a splashscreen-type loading window, which sometimes are allowed to hang out on top.
    # Qt.FramelessWindowHint asks to be made free of all window chrome and decoration. No close buttons.
    # Qt.WindowStaysOnTopHint asks to be allowed to stay on top of everything else.
    # Qt.WindowDoesNotAcceptFocus just says that we want all the attention to be somewhere else.
    
    callback = lambda e: sys.exit()
    #window.mouseMoveEvent = mousemove
    #window.mousePressEvent = callback
    window.mouseDoubleClickEvent = callback
    
    # Create the button
    ratetext = QLabel() # The label that holds the current heart rate.
    ratetext.setText("Loading...") # Let's make it say "Loading" while we're loading.
    ratetext.setStyleSheet('font-size: 20pt; font-weight: 100; color: rgba(200, 200, 200, 0.7);') # Some stylistic options.
    
    shadow = QGraphicsDropShadowEffect() # This is a drop shadow effect that we'll use as a weak outline.
    shadow.setColor(QColor(0, 0, 0, 200)) # Black shadow, slight transparency
    shadow.setBlurRadius(3) # Slight blur to make it actually visible around the edges because...
    shadow.setOffset(0, 0) # It's sitting directly below the text.
    ratetext.setGraphicsEffect(shadow) # And apply the effect.
    
    heart = QLabel() # The heart icon. 
    icon = '🖤' # I actually used an emoji for mine but I guess not everyone has emoji on their computers.
    sheet = 'min-width: 20pt; font-weight: 600;' # The style.
    heart.setText(icon) # Insert text
    heart.setStyleSheet(sheet) # apply styling
    
    hshadow = QGraphicsDropShadowEffect() # Let's apply that shadow to our heart as well.
    hshadow.setColor(QColor(0, 0, 0, 200)) 
    hshadow.setBlurRadius(3)
    hshadow.setOffset(0, 0)
    heart.setGraphicsEffect(hshadow)
    
    line = QLabel() # This will contain the picture of that fancy line thing.
    
    pic = QPicture() # This is the picture of that fancy line thing.
    
    paint = QPainter(pic) # This is the misunderstood artist who will be painting that fancy line thing.
    paint.setPen(QPen(Qt.white, 1, Qt.SolidLine, Qt.RoundCap)) # For a "loading" line, opaque white.
    paint.setRenderHint(QPainter.Antialiasing) # Turn on Antialiasing.
    paint.setRenderHint(QPainter.HighQualityAntialiasing) # "'HighQualityAntialiasing'? Sure that sounds nice, let's turn that on."
    paint.drawLine(0, 25, 150, 25) # Flatlined.
    paint.end() # And the painter is finished.
    
    vbox = QVBoxLayout() # This is our main layout.
    hbox = QHBoxLayout() # This is the "informational" layout on top with the rate and heart icon.
    
    hbox.addWidget(ratetext) # Add the heart rate to the horizontal box.
    hbox.addStretch(1) # Add a stretcher that will suck up as much space as it can.
    hbox.addWidget(heart) # Add the heart icon to the horizonal box.
    #hbox.addStretch(1) # And another stretcher, make them fight each other. The point of this is to basically "center" the heart icon in the leftover space.
    
    vbox.addLayout(hbox) # Add that horizontal box to the vertical box.
    vbox.addWidget(line) # Add that fancy line thing to the vertical box.
    window.setLayout(vbox) # And set the vertical box as our main layout here.
    
    window.resize(150, 20) # Resize the window to 150x20.
    
    window.move(200, 300) # Relocate it to the top left corner.
    #center()
    
    window.show() # Lights, camera, action.
    
    
    # And every time you update the GUI and need it to show, you just give it a little bit of this
    
    app.processEvents()
    
    sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

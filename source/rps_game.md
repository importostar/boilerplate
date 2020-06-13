---
title: rps_game
date: 2020-05-07
---
Example Python program rps_game.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5.QtWidgets import *
* from PyQt5.QtGui import QFont, QPixmap
* from PyQt5.QtCore import QTimer
* from random import randint

## Classes

* class Window(QWidget):

## Methods

* def __init__(self):
* def UI(self):
* def play_game(self):
* def start(self):
* def stop(self):
* def main():

## Code

Example Python PyQt program :

    # -*- coding: utf8 -*-
    # Programa: rps_game.py
    # Objetivo: Conocer PyQt5
    # Autor: Héctor Sabillón
    # Fecha: 10/marzo/2020
    
    import sys
    from PyQt5.QtWidgets import *
    from PyQt5.QtGui import QFont, QPixmap
    from PyQt5.QtCore import QTimer
    from random import randint
    
    
    # Declaración de variables
    text_font = QFont("Verdana", 14)
    button_font = QFont("Arial", 12)
    computer_score = 0
    player_score = 0
    
    
    class Window(QWidget):
        """ Muestra la ventana principal. """
    
        def __init__(self):
            """ Inicializador del objeto. """
            super().__init__()  # Manda a llamar al padre
            self.setWindowTitle("Piedra papel o tijera - El juego")
            self.setGeometry(350, 150, 550, 500)
            self.img_rock = QPixmap("img/rock.png")
            self.img_paper = QPixmap("img/paper.png")
            self.img_scissor = QPixmap("img/scissors.png")
            self.UI()
    
        def UI(self):
            """ Define los widgets que se muestran en la ventana. """
            # Puntajes
            self.score_computer_text = QLabel("Puntaje de la CPU: ", self)
            self.score_computer_text.move(30, 20)
            self.score_computer_text.setFont(text_font)
            self.score_player_text = QLabel("Tu puntaje: ", self)
            self.score_player_text.move(330, 20)
            self.score_player_text.setFont(text_font)
    
            # Botones
            btn_start = QPushButton("Inicio", self)
            btn_start.setFont(button_font)
            btn_start.move(180, 250)
            btn_start.clicked.connect(self.start)
            btn_stop = QPushButton("Detener", self)
            btn_stop.setFont(button_font)
            btn_stop.move(270, 250)
            btn_stop.clicked.connect(self.stop)
    
            # Imágenes
            self.img_vs = QLabel(self)
            # Obtener la imagen mediante una ruta relativa
            self.img_vs.setPixmap(QPixmap("img/game.png"))
            self.img_vs.move(230, 160)
    
            self.img_cpu = QLabel(self)
            self.img_cpu.setPixmap(self.img_rock)
            self.img_cpu.move(50, 100)
    
            self.img_player = QLabel(self)
            self.img_player.setPixmap(self.img_rock)
            self.img_player.move(330, 100)
    
            # Timer
            self.timer = QTimer(self)
            self.timer.setInterval(80)
            self.timer.timeout.connect(self.play_game)
    
            # Mostrar los elementos
            self.show()
    
        def play_game(self):
            """ Asigna de manera aletoria una imagen al cpu y al jugador """
            self.random_cpu = randint(1, 3)
            self.random_player = randint(1, 3)
    
            # Asignar las imágenes según el valora aleatorio
            if self.random_cpu == 1:
                self.img_cpu.setPixmap(self.img_rock)
            elif self.random_cpu == 2:
                self.img_cpu.setPixmap(self.img_paper)
            else:
                self.img_cpu.setPixmap(self.img_scissor)
    
            if self.random_player == 1:
                self.img_player.setPixmap(self.img_rock)
            elif self.random_player == 2:
                self.img_player.setPixmap(self.img_paper)
            else:
                self.img_player.setPixmap(self.img_scissor)
    
        def start(self):
            """ Inicializa el timer del juego """
            self.timer.start()
    
        def stop(self):
            """ Detener el timer del juego y evalua el resultado """
            self.timer.stop()
            global computer_score
            global player_score
    
            # Evaluar los resultados de las imágenes
            # CPU -> Rock vs Player
            if self.random_cpu == 1 and self.random_player == 1:
                message_box = QMessageBox.information(
                    self, "Información", "Empate")
            elif self.random_cpu == 1 and self.random_player == 2:
                player_score += 1
                self.score_player_text.setText(
                    "Tu puntaje: {0}".format(player_score))
                message_box = QMessageBox.information(
                    self, "Información", "Gana el jugador")
            elif self.random_cpu == 1 and self.random_player == 3:
                computer_score += 1
                self.score_computer_text.setText(
                    "Puntaje de la CPU: {0}".format(computer_score))
                message_box = QMessageBox.information(
                    self, "Información", "Gana el CPU")
            # CPU -> Paper vs Player
            elif self.random_cpu == 2 and self.random_player == 2:
                message_box = QMessageBox.information(
                    self, "Información", "Empate")
            elif self.random_cpu == 2 and self.random_player == 3:
                player_score += 1
                self.score_player_text.setText(
                    "Tu puntaje: {0}".format(player_score))
                message_box = QMessageBox.information(
                    self, "Información", "Gana el jugador")
            elif self.random_cpu == 2 and self.random_player == 1:
                computer_score += 1
                self.score_computer_text.setText(
                    "Puntaje de la CPU: {0}".format(computer_score))
                message_box = QMessageBox.information(
                    self, "Información", "Gana el CPU")
            # CPU -> Scissor vs Player
            elif self.random_cpu == 3 and self.random_player == 3:
                message_box = QMessageBox.information(
                    self, "Información", "Empate")
            elif self.random_cpu == 3 and self.random_player == 1:
                player_score += 1
                self.score_player_text.setText(
                    "Tu puntaje: {0}".format(player_score))
                message_box = QMessageBox.information(
                    self, "Información", "Gana el jugador")
            elif self.random_cpu == 3 and self.random_player == 2:
                computer_score += 1
                self.score_computer_text.setText(
                    "Puntaje de la CPU: {0}".format(computer_score))
                message_box = QMessageBox.information(
                    self, "Información", "Gana el CPU")
    
            # Verificar qui´en obtiene las 3 victorias
            if computer_score == 3:
                message_box = QMessageBox.information(
                    self, "Información", "El CPU es el ganador. Game Over")
                sys.exit()
            elif player_score == 3:
                message_box = QMessageBox.information(
                    self, "Información", "El jugador es el ganador. Game Over")
                sys.exit()
    
    
    def main():
        """ Ejecuta la aplicación """
        App = QApplication(sys.argv)
        window = Window()
        window.start()
        sys.exit(App.exec_())
    
    
    if __name__ == "__main__":
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

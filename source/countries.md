---
title: countries
date: 2020-05-07
---
Example Python program countries.py
This program creates a PyQt GUI

## Modules

* import sys
* import csv
* from PyQt5.QtWidgets import QApplication, QMainWindow, QMessageBox
* from PyQt5.QtGui import QPixmap
* import worldCountriesLIB

## Classes

* class MyForm(QMainWindow, worldCountriesLIB.Ui_MainWindow):

## Methods

* def __init__(self, parent=None):
* def loadCountries(self):
* def changeCountry(self, newIndex):
* def exitProgram(self):
* def updateCountryPopulation(self):
* def updatePopulationDensity(self):
* def changeAreaDisplay(self, newIndex):
* def loadCountriesFromFile(self):
* def loadCountriesIntoWidget(self):
* def saveChangesToMemory(self):
* def calculateTotalPopulation(self):
* def saveChangesToFile(self):
* def showMilesDensity(self):
* def showKiloDensity(self):

## Code

Example Python PyQt program :

    import sys
    import csv
    
    from PyQt5.QtWidgets import QApplication, QMainWindow, QMessageBox
    from PyQt5.QtGui import QPixmap
    
    #ADD IMPORT STATEMENT FOR YOUR GENERATED UI.PY FILE HERE
    import worldCountriesLIB
    
    #CHANGE THE SECOND PARAMETER HERE TO MATCH YOUR GENERATED UI.PY FILE
    class MyForm(QMainWindow, worldCountriesLIB.Ui_MainWindow):
    
        # --- Variables that will be used throughout the program ---
        changesMade = False             # Will keep track of changes made to prompt saving
        totalPopulation = 0             # Used in calculating the total population loaded from the text file
    
            # DO NOT MODIFY THIS CODE
        def __init__(self, parent=None):
            super(MyForm, self).__init__(parent)
            self.setupUi(self)
            # END DO NOT MODIFY
    
            # ADD SLOTS HERE
            self.actionLoadCountries.triggered.connect(self.loadCountries)
            self.actionExitProgram.triggered.connect(self.exitProgram)
            self.listWidgetCountry.currentRowChanged.connect(self.changeCountry)
            self.pushButtonPopulationUpdate.clicked.connect(self.updateCountryPopulation)
            self.radioButtonMiles.clicked.connect(self.showMilesDensity)
            self.radioButtonKilometers.clicked.connect(self.showKiloDensity)
            self.comboBoxArea.currentIndexChanged.connect(self.changeAreaDisplay)
    
            self.frameCountryInfo.hide()
    
        # ADD SLOT FUNCTIONS HERE
        # Triggered when country data is loaded in using the menu
        def loadCountries(self):
            self.loadCountriesFromFile()
            self.loadCountriesIntoWidget()
    
        # Triggers when a user selects a country from the list
        def changeCountry(self, newIndex):
            countryName = self.countryList[newIndex][0].lower()
            flagImage = QPixmap("Flags\\" + countryName.replace(" ", "_"))
            populationPercent = (int(self.countryList[newIndex][1]) / self.totalPopulation) * 100
            self.frameCountryInfo.show()
            self.labelCountryName.setText(self.countryList[newIndex][0])
            self.lineEditPopulationValue.setText("{:,}".format(int(self.countryList[newIndex][1])))
            self.labelAreaValue.setText("{:,}".format(int(self.countryList[newIndex][2])))
            self.labelFlagDisplay.setPixmap(flagImage)
            self.labelPopulationPercentValue.setText("{:,}%".format(round(populationPercent, 4)))
            self.comboBoxArea.setCurrentIndex(0)
            self.updatePopulationDensity()
    
    
        # Triggers when the user selects exit from the menu
        def exitProgram(self):
            # Will check if changes have been made to prompt user to save to file
            if self.changesMade:
                saveChanges = QMessageBox.question(self, "Save Changes?",
                                     "There are unsaved changes, would you like to save before exiting?",
                                     QMessageBox.Yes, QMessageBox.No)
            if saveChanges == QMessageBox.Yes:
                self.saveChangesToFile()
            QApplication.closeAllWindows()
    
        # Triggers when the update button is clicked
        def updateCountryPopulation(self):
            self.saveChangesToMemory()
            self.changesMade = True             # Flags that a change has been made
    
        # Triggers when a new country is selected
        def updatePopulationDensity(self):
            if self.radioButtonMiles.isChecked() == True:           # Checking radio buttons for correct display
                self.showMilesDensity()
            elif self.radioButtonKilometers.isChecked() == True:    # Checking radio buttons for correct display
                self.showKiloDensity()
    
        # Triggers when a country is selected
        # Defaults to square miles
        def changeAreaDisplay(self, newIndex):
            currentRow = self.listWidgetCountry.currentRow()
            if newIndex == 0:                                       # Checking combo box for correct display
                countryArea = int(self.countryList[currentRow][2])
            elif newIndex == 1:                                     # Checking combo box for correct display
                countryArea = int(int(self.countryList[currentRow][2]) * 2.58999)
            self.labelAreaValue.setText("{:,}".format(countryArea))
    
        #ADD HELPER FUNCTIONS HERE
        # Used to read data from the text file
        def loadCountriesFromFile(self):
            fileName = "countries.txt"
            accessMode = "r"
            with open(fileName, accessMode) as countryFile:
                countryData = csv.reader(countryFile)
    
                self.countryList = []
                for item in countryData:
                    self.countryList.append(item)
    
        # Populates the list widget from the data collected from the text file
        def loadCountriesIntoWidget(self):
            self.listWidgetCountry.clear()
            for country in self.countryList:
                self.listWidgetCountry.addItem(country[0])
            self.calculateTotalPopulation()
    
        # Saves user inputted data to memory only
        def saveChangesToMemory(self):
            currentRow = self.listWidgetCountry.currentRow()
            # --- Error checking ---
            # User must enter a value
            # Value entered must be an integer value(or converted to an integer) before saving
            try:
                updatedPopulation = self.lineEditPopulationValue.text().replace(",", "")
                if updatedPopulation == "":
                    QMessageBox.information(self, "Error", "Please enter a value before updating.", QMessageBox.Ok)
                else:
                    self.countryList[currentRow][1] = int(updatedPopulation)
                    QMessageBox.information(self, "Message", "Population Updated", QMessageBox.Ok)
            except ValueError:
                QMessageBox.information(self, "Error", "Invalid entry for population total.", QMessageBox.Ok)
            self.loadCountriesIntoWidget()
            self.listWidgetCountry.setCurrentRow(currentRow)
    
        # Runs when country data is loaded into the widget
        def calculateTotalPopulation(self):
            self.totalPopulation = 0
            for row in self.countryList:
                self.totalPopulation += int(row[1])
    
        # Saves user inputted data to the text file
        def saveChangesToFile(self):
            fileName = "countries.txt"
            accessMode = "w"
            with open(fileName, accessMode) as newCountryFile:
                for row in self.countryList:
                    newCountryFile.write(",".join(row) + "\n")
            self.changesMade = False                # Flags that any changes made have been saved
            QMessageBox.information(self, "Data Saved", "Your changes have been saved.", QMessageBox.Ok)
    
        # Triggers when the radio button is clicked
        def showMilesDensity(self):
            currentRow = self.listWidgetCountry.currentRow()
            currentPopulation = int(self.countryList[currentRow][1])
            currentArea = int(self.countryList[currentRow][2])
            self.labelPopulationDensityValue.setText(str(round(currentPopulation / currentArea, 4)))
    
        # Triggers when the radio button is clicked
        def showKiloDensity(self):
            currentRow = self.listWidgetCountry.currentRow()
            currentPopulation = int(self.countryList[currentRow][1])
            currentArea = int(self.countryList[currentRow][2]) * 2.58999
            self.labelPopulationDensityValue.setText(str(round(currentPopulation / currentArea, 4)))
    
    # DO NOT MODIFY THIS CODE
    if __name__ == "__main__":
        app = QApplication(sys.argv)
        the_form = MyForm()
        the_form.show()
        sys.exit(app.exec_())
    # END DO NOT MODIFY

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

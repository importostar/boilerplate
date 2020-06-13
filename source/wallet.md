---
title: wallet
date: 2020-05-07
---
Example Python program wallet.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from PyQt5.QtGui import *
* from PyQt5.QtWidgets import *
* from PyQt5.QtCore import *
* import wallet_ui
* import web3
* import eth_account
* #from web3 import Web3
* #from eth_account import Account

## Classes

* class Wallet(QMainWindow, wallet_ui.Ui_MainWindow):

## Methods

* def __init__(self):
* def openFileNameDialog(self):
* def loadKeyFile(self, fileName):
* def decryptKeyFile(self, keyfile_json, passphrase):
* def sendTransaction(self):

## Code

Example Python PyQt program :

    #!/usr/bin/python3
    
    import sys
    from PyQt5.QtGui import *
    from PyQt5.QtWidgets import *
    from PyQt5.QtCore import *
    
    import wallet_ui
    
    import web3
    import eth_account
    #from web3 import Web3
    #from eth_account import Account
    
    class Wallet(QMainWindow, wallet_ui.Ui_MainWindow):
        def __init__(self):
            super().__init__()
            self.setupUi(self)
    
            self.actionOpen.triggered.connect(self.openFileNameDialog)
            self.sendButton.clicked.connect(self.sendTransaction)
            self.actionExit.triggered.connect(qApp.quit)
    
            self.web3 = web3.Web3(web3.Web3.HTTPProvider("http://127.0.0.1:8545"))
    
        def openFileNameDialog(self):    
            options = QFileDialog.Options()
            fileName, _ = QFileDialog.getOpenFileName(self, "Select wallet", "", "All Files (*)", options=options)
            if fileName:
                self.loadKeyFile(fileName)
    
        def loadKeyFile(self, fileName):
            with open(fileName) as keyfile:
                keyfile_json = keyfile.read()
                
                passphrase, okPressed = QInputDialog.getText(self, "Decrypt wallet", "Passphrase:", QLineEdit.Password, "")
                if okPressed and passphrase != '':
                    self.decryptKeyFile(keyfile_json, passphrase)
    
        def decryptKeyFile(self, keyfile_json, passphrase):
            #try:
                self.private_key = eth_account.Account.decrypt(keyfile_json, passphrase)
                self.acct = eth_account.Account.privateKeyToAccount(self.private_key)
    
                self.accountLineEdit.setText(self.acct.address)
    
                balance = self.web3.fromWei(self.web3.eth.getBalance(self.acct.address), 'ether')
                self.balanceLineEdit.setText("%0.6f" % (balance))
            #except ValueError:
            #    print(ValueError)
            #    QMessageBox.warning(self, 'Wallet decrypt error', "Broken wallet of invalid passphrase")
           
        def sendTransaction(self):
            to = self.sendToLineEdit.text()
            amount = self.amountSendLineEdit.text()
    
            if to != '' and amount != '':
    
                tx = dict(
                    nonce = self.web3.eth.getTransactionCount(self.acct.address),
                    gasPrice = self.web3.eth.gasPrice,
                    gas = 100000,
                    to = to,
                    value = self.web3.toWei(amount, 'ether'),
                    data = b''
                )
                signedTX = self.web3.eth.account.signTransaction(tx, self.private_key)
                txHash = self.web3.eth.sendRawTransaction(signedTX.rawTransaction)
                QMessageBox.information(self, "Transaction", txHash.hex())
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        win = Wallet()
        win.statusBar().setSizeGripEnabled(False)
        win.setFixedSize(807, 239)
        win.show()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

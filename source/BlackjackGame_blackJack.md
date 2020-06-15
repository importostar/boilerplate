---
title: BlackjackGame_blackJack
date: 2020-05-07
---
Example Python program BlackjackGame_blackJack.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import random
* import tkinter

## Methods

* def load_cards(card_images):
* def deal_cards(frame):
* def player_deal_cards():

## Code

Python tkinter example

    import random
    import tkinter
    
    
    def load_cards(card_images):
        suits = ["heart", "club", "diamond", "spade"]
        face_cards = ["jack", "king", "queen"]
    
        # for each suit, retrieve the image for the cards
        for suit in suits:
            # first the number cards 1 to 10
            for card in range(1, 11):
                name = 'cards/{}_{}.png'.format(str(card), suit)
                image = tkinter.PhotoImage(file=name)
                card_images.append((card, image,))
    
            # next the face cards
            for card in face_cards:
                name = 'cards/{}_{}.png'.format(str(card), suit)
                image = tkinter.PhotoImage(file=name)
                card_images.append((10, image,))
    
    
    def deal_cards(frame):
        # pop the next card off the top of the deck
        next_card = deck.pop(0)
        # add the image to a label and display the label
        tkinter.Label(frame, image=next_card[1], relief="raised").pack(side='left')
        # now return the card's face value
        return next_card
    
    
    def player_deal_cards():
        global player_score
        global player_has_ace
        card_value = deal_cards(playerCardFrame)[0]
        if card_value == 1 and not player_has_ace:
            card_value = 11
        player_score += card_value
        if player_score > 21 and player_has_ace:
            player_score -= 10
            player_has_ace = False
        playerScoreLabel.set(player_score)
        if player_score > 21:
            resultText.set("Dealer Wins")
    
    
    mainWindow = tkinter.Tk()
    
    # set-up the screen for Dealer and Player
    mainWindow.title("Black Jack")  # setting the the title
    mainWindow.geometry("640x480")  # specifying the width and height of the panel
    
    # Providing the Winner Name (Player or Dealer) at the top row
    resultText = tkinter.StringVar()
    result = tkinter.Label(mainWindow, textvariable=resultText)
    result.grid(row=0, column=0, columnspan=3)
    
    # Building a Card-Frame inside the mainWindow
    cardFrame = tkinter.Frame(mainWindow, borderwidth=1, background="green")
    cardFrame.grid(row=1, column=0, sticky='ew', columnspan=3, rowspan=2)
    
    # Dealer label and score
    tkinter.Label(cardFrame, text="Dealer", background="green", fg="white").grid(row=0, column=0)
    dealerScoreLabel = tkinter.IntVar()
    tkinter.Label(cardFrame, textvariable=dealerScoreLabel, background="green", fg="white").grid(row=1, column=0)
    
    # Player label and score
    tkinter.Label(cardFrame, text="Player", background="green", fg="white").grid(row=2, column=0)
    playerScoreLabel = tkinter.IntVar()
    player_score = 0
    player_has_ace = False
    tkinter.Label(cardFrame, textvariable=playerScoreLabel, background="green", fg="white").grid(row=3, column=0)
    
    # Card Frame for holding Cards
    dealerCardFrame = tkinter.Frame(cardFrame, background="green")
    dealerCardFrame.grid(row=0, column=1, sticky="ew", rowspan=2)
    playerCardFrame = tkinter.Frame(cardFrame, background="green")
    playerCardFrame.grid(row=2, column=1, sticky="ew", rowspan=2)
    
    # Button Frame for Dealer and Player
    buttonFrame = tkinter.Frame(mainWindow)
    buttonFrame.grid(row=3, column=0, columnspan=3, sticky='w')
    
    # Dealer Button
    dealerButtonFrame = tkinter.Button(buttonFrame, text="Dealer", command=lambda: deal_cards(dealerCardFrame))
    dealerButtonFrame.grid(row=0, column=0)
    
    # Player Button
    playerButtonFrame = tkinter.Button(buttonFrame, text="Player", command=player_deal_cards)
    playerButtonFrame.grid(row=0, column=1)
    
    # load cards
    cards = []
    load_cards(cards)
    print(cards)
    
    # Create a new deck of cards and shuffle them
    deck = list(cards)
    random.shuffle(deck)
    
    # Create the list to store the dealer's and player's hands
    dealer_hand = []
    player_hand = []
    
    mainWindow.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

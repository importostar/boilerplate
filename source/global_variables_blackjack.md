---
title: global_variables_blackjack
date: 2020-05-07
---
Example Python program global_variables_blackjack.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import random
* import tkinter

## Methods

* def load_images(card_images):  #incarca imaginile cu cartile
* def deal_card(frame):
* def score_hand(hand):
* def deal_dealer():
* def deal_player():
* def new_game():
* def shuffle():

## Code

Python tkinter example

    #imaginile le gasesti aici
    # http://svg-cards.sourceforge.net/
    #=====GLOBAL  VARIABLES============
    
    import random
    import tkinter
    
    def load_images(card_images):  #incarca imaginile cu cartile
    	suits= ['heart', 'club', 'diamond', 'spade']  #case sensitive
    	face_cards= ['jack', 'queen', 'king']
    	#apoi verificam ce versiune de tkinter folosim
    	#pt ca doar dupa 8.5 merge sa folosesti .png
    	#eu oricum nu folosesc PNG dar e bine de avut
    	if tkinter.TkVersion >= 8.6:
    		extension = 'ppm' #puneai aici png daca aveai pozele si in formatul ala
    	else:
    		extension = 'ppm' 
    
    	#for each suit, retrive the image for the cards
    	for suit in suits:
    		#first the number cards 1 to 10
    		for card in range(1,11):
    			name = 'cards\{}_{}.{}'.format(str(card), suit, extension)  #cards e directorul in care avem pozele
    			image = tkinter.PhotoImage(file= name)
    			card_images.append((card, image))
    
    		#next the face cards
    		for card in face_cards:
    			name = 'cards\{}_{}.{}'.format(str(card), suit, extension) #daca esti pe linux/mac pui cards/, nu cards\ ca pe win
    			image = tkinter.PhotoImage(file = name)
    			card_images.append((10, image))
    
    
    def deal_card(frame):
    	#pop the next card of the top of the deck
    	next_card = deck.pop(0)  #pop retrieves an item from the END of the list, and also removes it 
    						#opusul lui append
    						#insa, daca ii pui zero la argument in paranteza, o ia pe prima din pachet
    
    	#and add it to the back of the pack
    	deck.append(next_card)  #daca nu pui linis asta si dai de multe ori new game
    				#ramai fara carti in pachet si va da eroare... dupa cateva jocuri						
    
    	#add the image to a label and display a label
    	tkinter.Label(frame, image= next_card[1], relief= 'raised').pack(side= 'left')
    	#now return the card's face value
    	return next_card
    	#it's a bad ideea to mix grid and pack in the same window
    
    
    def score_hand(hand):
    	#Calculate the total score of all cards in the list
    	#only 1 Ace can have the value of 11
    	#and the value of the Ace will be reduced to one if the hand will bust
    	score = 0
    	ace = False
    	for next_card in hand:
    		#ia cartile la rand
    		card_value = next_card[0] #prima carte
    		if card_value == 1 and not ace: #ace e False in momentul asta
    			ace = True
    			card_value = 11 #daca e singurul as, are 11 puncte
    		score += card_value
    		#if we would bust, check if there is an ace 
    		#and substract 10 if you find one (Ace)
    		if score > 21 and ace:  #daca ai scor >21 si ai as in mana
    			score -= 10
    			ace = False
    	return score
    
    
    def deal_dealer():
    	dealer_score = score_hand(dealer_hand)
    	while 0 < dealer_score < 17: #daca scorul e sub 17, dealerul
    				#primeste automat inca o carte
    		dealer_hand.append(deal_card(dealer_card_frame))
    		dealer_score = score_hand(dealer_hand)
    		dealer_score_label.set(dealer_score)  #show it on the screen
    
    	player_score = score_hand(player_hand)
    	if player_score > 21:
    		result_text.set("Dealer Wins!")
    	elif dealer_score > 21 or dealer_score < player_score:
    		result_text.set("Scorpion Wins! -player-")
    	elif dealer_score > player_score:
    		result_text.set("dealer wins!")
    	else:
    		result_text.set("Draw !")
    
    
    def deal_player():
    	player_hand.append(deal_card(player_card_frame))
    	player_score =  score_hand(player_hand)
    	player_score_label.set(player_score)
    	if player_score > 21:
    		result_text.set("SUB-ZERO wins! -dealer-")
    
    def new_game():
    	global dealer_card_frame
    	global player_card_frame
    	global dealer_hand
    	global player_hand
    	#embedded frame to hold the card images for the dealer
    	dealer_card_frame.destroy() # to clear the score from prev game
    	dealer_card_frame = tkinter.Frame(card_frame, background = 'green')
    	dealer_card_frame.grid(row = 0, column =1, sticky = 'ew', rowspan = 2)
    	#embedded frame to hold the card images for the player
    	player_card_frame.destroy() # to clear the score from prev game
    	player_card_frame = tkinter.Frame(card_frame, background = 'green')
    	player_card_frame.grid(row = 2, column =1, sticky = 'ew', rowspan = 2)
    
    	result_text.set("")  #empty string to clear the result from prev game
    
    	#create the list to store dealer`s and player's hand
    	dealer_hand = []
    	player_hand = []
    
    	deal_player()  #pleier primeste automat prima carte
    	dealer_hand.append(deal_card(dealer_card_frame))
    	dealer_score_label.set(score_hand(dealer_hand))
    	deal_player()
    
    	
    
    	"""
    	mai jos ai vechea varianta de deal_player
    	#daca totusi vrei sa modifici o variabila globala in interiorul unei functii
    	#folosesti keyword global, vor fi folosite variabelele globale
    	#si nu vor mai fi create variabile locale cu acelasi nume
    	global player_score
    	global player_ace
    	card_value = deal_card(player_card_frame)[0]
    	if card_value == 1 and not player_ace:
    		
    		player_ace = True #cand ai un as o setezi true, pt cazul in care iti pica si al doilea
    					#as, asa o sa stie si o sa puna al doilea as 1, nu 11 puncte
    		card_value = 11 #asta verifica daca mai ai sau nu un as
    				#daca nu ai, asul tau va valora 11 puncte 
    				#daca ai 2 asi, al doilea valoreaza 1 punct, ca sa nu faci peste 21
    	player_score += card_value
    	#if we would bust(faci peste 21), check if there is an ace, and substract 10
    	#aka il faci 1 pe al doilea as din mana
    	if player_score > 21 and player_ace: #player_ace verifica daca ai un as in mana
    		player_score -= 10
    		player_ace = False
    	player_score_label.set(player_score) 
    	if player_score > 21:
    		result_text.set("Dealer wins!")
    	print(locals()) #printeaza TOATE variabilele locale
    	"""
    
    	#player_ace is set True if that would be necessary to prevent the player 
    	#going bust. If it's False, the ace counts as 11, otherwise it counts as 1.
    	#That check is repeated for each ace found. If the player would go bust and 
    	#has an ace, 10 is subtracted from the score (making the ace worth 1 instead of 11).
    
    	#PITONELE TE LASA SA FOLOSESTI O VARIABILA GLOBALA INTR-O FUNCTIE
    	#PANA CAND VREI SA II MODIFICI VALOAREA IN FUNCTIA RESPECTIVA 
    	#CAND II MODIFICI VALOAREA IN FUNCTIE, PITONELE CREEAZA AUTOMAT O VAR LOCALA
    	#CU ACELASI NUME SI CODUL TAU NU SE MAI REFERA LA VAR GLOBALA
    
    	#exceptia este APPEND, daca faci append, nu faci shadowing si deci nu da eroare in caz ca pui o var globala
    	#intr-o functie fara sa folosesti keyword global
    	#atat player_hand[] cat si dealer_hand[] sunt initializate ca liste, continua sa faca referinta la aceleasi liste
    	#cat timp programul ruleaza, ADDING OR REMOVING ITEMS FROM A LIST IS NOT 
    	#MODIFYING the list variable
    
    	#player_score_label isn't given a value in the function, it continues to refer to exactly 
    	#the same widget all the time.
    	#Calling its set function to make the widget display different text isn't 
    	#the same as changing the variable.
    	#That will make more sense when we cover classes, later in the course.
    
    def shuffle():
    	random.shuffle(deck)  #execute random.shuffle for the deck
    
    mainWindow = tkinter.Tk()
    
    #set up the screen and frames for the dealer and player
    mainWindow.title("Black Jack")
    mainWindow.geometry("640x480")
    mainWindow.configure(background='green')
    
    result_text = tkinter.StringVar()
    result = tkinter.Label(mainWindow, textvariable = result_text)
    result.grid(row= 0, column= 0, columnspan= 3)
    
    card_frame = tkinter.Frame(mainWindow, relief='sunken', borderwidth=1, background = 'green')
    card_frame.grid(row=1, column=0, sticky = 'ew', columnspan= 3, rowspan= 2)
    
    dealer_score_label = tkinter.IntVar()
    tkinter.Label(card_frame, text='Dealer', background= 'green', fg= 'white').grid(row=0, column=0)
    tkinter.Label(card_frame, textvariable= dealer_score_label, background='green', fg='white').grid(row= 1, column= 0)
    
    #embeded frame to hold the card images
    dealer_card_frame= tkinter.Frame(card_frame, background= 'green')
    dealer_card_frame.grid(row= 0, column= 1, sticky= 'ew', rowspan= 2)
    
    player_score_label = tkinter.IntVar()
    #variables that are defined NOT IN A FUNCTION, are called GLOBAL V
    #variables that are defined IN A FUNCTIONS, are called LOCAL V
    
    tkinter.Label(card_frame, text= 'Player', background= 'green', fg='white').grid(row=2, column=0)
    tkinter.Label(card_frame, textvariable= player_score_label, background= 'green', fg= 'white').grid(row= 3, column= 0)
    
    #embedded frame to hold the card images
    player_card_frame = tkinter.Frame(card_frame, background= 'green')
    player_card_frame.grid(row=2, column= 1, sticky= 'ew', rowspan= 2) #ew adica pe toata latimea
    
    button_frame = tkinter.Frame(mainWindow)
    button_frame.grid(row= 3, column= 0, columnspan= 3, sticky='w')
    
    
    #be carefull when setting up the command property of widgets, the value that you assign has to be the function
    #that you want to be executed when the button is clicked
    dealer_button = tkinter.Button(button_frame, text= 'Dealer', command= deal_dealer) #daca incluzi parantezele dupa numele functiei
    							#you're asigning the result of calling the function, rather than asigning the function itself
    							#and assigning the function itself is what you want
    dealer_button.grid(row= 0, column=0)
    
    player_button = tkinter.Button(button_frame, text= 'Player', command = deal_player)
    player_button.grid(row= 0, column =1)
    
    new_game_button = tkinter.Button(button_frame, text= 'New game', command = new_game)
    new_game_button.grid(row = 0, column = 2)
    
    shuffle_button = tkinter.Button(button_frame, text = 'Shuffle Cards', command = shuffle)
    shuffle_button.grid(row =0, column = 3)
    
    #load cards
    cards = []
    load_images(cards)
    print(cards)
    
    #create a new deck of cards and shuffle them
    #shuffle e din modulul random
    deck = list(cards)  #daca puneai aici deck=cards, la fiecare 'mana' 
    			#ramaneau din ce in ce mai putine carti
    			
    		#pt a juca cu mai multe 'pachete ' de carti poti face asa:
    	# deck = list(cards) + list(cards) + list(cards)
    
    shuffle()
    
    #create the list to store dealer`s and player's hand
    dealer_hand = []
    player_hand = []
    new_game()
    
    mainWindow.mainloop()
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

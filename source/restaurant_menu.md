---
title: restaurant_menu
date: 2020-05-07
---
Example Python program restaurant_menu.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tkinter  # Need to import tkinter for making a GUI
* import tkinter.messagebox   # Needed for the tkinter messagebox
* import time # Needed to display current time and date

## Classes

* class MyGUI:

## Methods

* def __init__(self):
* def see_drinks(self):
* def drinkWater(self):
* def drinkDP(self):
* def drinkCoke(self):
* def drinkRB(self):
* def drinkTea(self):
* def show_drinkChoice(self):
* def drnk_option1(self):
* def drnk_option2(self):
* def drnk_option3(self):
* def drnk_option4(self):
* def drnk_option5(self):
* def see_appetizers(self):
* def appetSalsa(self):
* def appetSpinDip(self):
* def appetNachos(self):
* def appetWings(self):
* def appetORings(self):
* def show_appetChoice(self):
* def appet_option1(self):
* def appet_option2(self):
* def appet_option3(self):
* def appet_option4(self):
* def appet_option5(self):
* def see_lunchMenu(self):
* def lunchBurger1(self):
* def lunchBurger2(self):
* def lunchChicken(self):
* def lunchBLT(self):
* def lunchSoup(self):
* def show_lunchChoice(self):
* def lunch_option1(self):
* def lunch_option2(self):
* def lunch_option3(self):
* def lunch_option4(self):
* def lunch_option5(self):
* def see_dinnerMenu(self):
* def dinnerSteak(self):
* def dinnerQuesadilla(self):
* def dinnerChickenS(self):
* def dinnerCrawfish(self):
* def dinnerRestBurger(self):
* def show_dinnerChoice(self):
* def dinner_option1(self):
* def dinner_option2(self):
* def dinner_option3(self):
* def dinner_option4(self):
* def dinner_option5(self):
* def see_desserts(self):
* def dessertIceCream(self):
* def dessertBBCcake(self):
* def dessertMilkshake(self):
* def dessertCake(self):
* def dessertRBfloat(self):
* def show_dessertChoice(self):
* def dessert_option1(self):
* def dessert_option2(self):
* def dessert_option3(self):
* def dessert_option4(self):
* def dessert_option5(self):
* def checkout(self):

## Code

Python tkinter example

    # -----------------------------------------------------------------------------------
    # Course: COSC-1436 - Python
    # Student: physicsCat1983
    # Assignment: Project - Restaurant Menu
    # -----------------------------------------------------------------------------------
    
    import tkinter              # Need to import tkinter for making a GUI
    import tkinter.messagebox   # Needed for the tkinter messagebox
    import time                 # Needed to display current time and date
    
    class MyGUI:
        
        # *******************************************************************************
        # The __init__ method builds the GUI.
        # *******************************************************************************
        
        def __init__(self):
            
            # ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            # Initialized variables for the program.
            self.price = 0
            self.flag_1 = 0
            self.flag_2_1 = 0
            self.flag_2_2 = 0
            self.flag_2_3 = 0
            self.flag_2_4 = 0
            self.flag_2_5 = 0
            self.flag_3 = 0
            self.flag_4 = 0
            self.flag_5 = 0
    
            # Initialize dictionaries for the program.
            self.drink_items = {'H2O':'Fresh water comes with meal.\nPrice: $0', \
                                'DP':'Dr. Pepper, Be The Pepper.\nPrice: $0.99', \
                                'Coke':'Classic Coca Cola\nPrice: $0.99', \
                                'RB':'Root Beer Classic\nPrice: $0.99', \
                                'Tea':'Sweetened & Unsweatened Tea\nPrice: $0.89'}
            self.appet_items = {'Salsa':'Made in house salsa\nserved with corn chips.\nPrice: $1.00', \
                                'SpinDip':'Made in house spinach dip\nserved with salted crackers.\nPrice: $1.50', \
                                'Nachos':'Classic melted cheese and jalapenos\ncovered on corn chips.\nPrice: $1.00', \
                                'Wings':'Buffalo wings drenched with\nsecret spicy sauce.\nPrice: $2.50', \
                                'ORings':'Sliced, seasoned battered, and fried\nonion rings served with\nhorseradish dipping sauce.\nPrice: $1.75'}
            self.lunch_items = {'Burg1':'Cheese Burger with American cheese\non American grade-A beef\nPrice: $3.25', \
                                'Burg2':'Bacon Cheese Burger\nMade with all American choice products.\nPrice: $3.50', \
                                'GrldChkn':'Seasoned Grilled Chicken served with\na side of veggies.\nPrice: $4.00', \
                                'BLT':'Classic BLT Sandwich\nBacon-Lettuce-Tomato\nPrice: $3.00', \
                                'SS':'Soup & Salad\nYour choice of Tomato or Chicken Noodle Soup\nserved with saltine crackers and a house salad.\nPrice: $2.65'}
            self.dinner_items = {'Steak':'Fire Grilled Steak\n8oz. Ribeye Steak Seasoned and cooked to perfection.\nComes with a baked potato.\nPrice: $8.50', \
                                 'Quesadillas':'Your choice of beef, chicken, pork, or shrimp.\nServed with baked beans and Mexican rice.\nPrice: $4.75', \
                                 'Chicken Salad':'Romaine Lettuce with cherry tomatoes and sliced onion\nand sliced seasoned chick.\nLarge choice of dressings.\nPrice: $4.00', \
                                 'Crawfish':'3 pounds of our signature Cajun Style Crawfish Boil\nPrice: $18.00', \
                                 'The Restaurant Burger':'TOP SECRET:\nOur secret special reciped burger\nmade our secret special way.\nPrice: $4.00'}
            self.dessert_items = {'Homemade Vanilla Ice Cream':'Homemade Vanilla Ice Cream\nPrice: $1.50', \
                                  'Blueberry Cheesecake':'Cheesecake served with a blueberry drizzle and blueberries on top.\nPrice: $2.00', \
                                  'Chocolate Milkshake':'Our Classic Chocolate Milkshake\nPrice: $1.75', \
                                  'Carrot Cake':'Homemade Carrot Cake\nPrice: $2.00', \
                                  'Root Beer Float':'Classic Root Beer Float.\nVanilla Ice Cream drowned in Root Beer.\nPrice: $1.90'}
            # ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            
            # Create the main window widget.
            self.main_window = tkinter.Tk()
    
            # Create a title for the main window.
            self.main_window.title('The Restaurant')
    
            # Resize the main window.
            self.main_window.geometry('1000x800')
    
            # ---------------------------------------------------------------------------
            # Create two frames, one for the top of
            # the window, and one for the bottom
            # and pack both of them in.
            # ---------------------------------------------------------------------------
            self.image2_frame = tkinter.Frame(self.main_window)
            self.top_frame = tkinter.Frame(self.main_window)
            self.bottom_frame = tkinter.Frame(self.main_window)
            self.image_frame = tkinter.Frame(self.main_window)
            self.image_frame.pack()
            self.top_frame.pack()
            self.bottom_frame.pack()
            self.image2_frame.pack()
    
            # ---------------------------------------------------------------------------
            # Create a blank label for a space in
            # the image_frame.
            # ---------------------------------------------------------------------------
            self.blankLabel_img = tkinter.Label(self.image_frame)
    
            # Pack blankLabel_img.
            self.blankLabel_img.pack()
    
            # ---------------------------------------------------------------------------
            # Add PhotoImage widget to the image_frame.
            # ---------------------------------------------------------------------------
    
            # Restaurant image
            self.rest_photo = tkinter.PhotoImage(file='restaurant2.gif')
            self.img_label1 = tkinter.Label(self.image_frame, image=self.rest_photo).pack(side='left')
    
            # ---------------------------------------------------------------------------
            # Create a label widget containing
            # the text "Welcome to The Restaurant".
            # ---------------------------------------------------------------------------
            self.label_1 = tkinter.Label(self.top_frame, \
                                         text='Welcome to The Restaurant', \
                                         bg='dark blue', fg='white', \
                                         font='Helvetica 24 bold')
            # Pack label_1.
            self.label_1.pack()
    
            # ---------------------------------------------------------------------------
            # Create a label widget containing
            # the text "The Restaurant Menu".
            # ---------------------------------------------------------------------------
            self.label_2 = tkinter.Label(self.bottom_frame, \
                                         text='The Restaurant Menu', \
                                         bg='dark blue', fg='white', \
                                         font='Helvetica 18 bold')
            # Pack label_2.
            self.label_2.pack()
    
            # ---------------------------------------------------------------------------
            # Create a blank label for a space in
            # the top frame.
            # ---------------------------------------------------------------------------
            self.blankLabel_1 = tkinter.Label(self.top_frame)
    
            # Pack blankLabel_1.
            self.blankLabel_1.pack()
    
            # ---------------------------------------------------------------------------
            # Create a blank label for a space in
            # the bottom frame.
            # ---------------------------------------------------------------------------
            self.blankLabel_2 = tkinter.Label(self.bottom_frame)
    
            # Pack blankLabel_2.
            self.blankLabel_2.pack()
    
            # ---------------------------------------------------------------------------
            # Create some Button widgets in the
            # bottom frame to establish the choices 
            # on the menu: Drinks, Appetizers,
            # Lunch Menu, Dinner Menu, and Desserts
            # ---------------------------------------------------------------------------
            
            # ~~~~~~~~~~~~~~~~~~~~~~~~ Drinks ~~~~~~~~~~~~~~~~~~~~~~~~~~~
            self.drinks_button = tkinter.Button(self.bottom_frame, \
                                                text='DRINKS', \
                                                command=self.see_drinks, \
                                                bg='green', fg='white', \
                                                font='Helvetica 12 bold', \
                                                width=15, height=2)
            # Pack the drinks Button.
            self.drinks_button.pack(side='left')
    
            # ~~~~~~~~~~~~~~~~~~~~~~ Appetizers ~~~~~~~~~~~~~~~~~~~~~~~~~
            self.appetizers_button = tkinter.Button(self.bottom_frame, \
                                                    text='APPETIZERS', \
                                                    command=self.see_appetizers, \
                                                    bg='green', fg='white', \
                                                    font='Helvetica 12 bold', \
                                                    width=15, height=2)
            # Pack the appetizers Button.
            self.appetizers_button.pack(side='left')
    
            # ~~~~~~~~~~~~~~~~~~~~~~ Lunch Menu ~~~~~~~~~~~~~~~~~~~~~~~~~
            self.lunch_button = tkinter.Button(self.bottom_frame, \
                                               text='LUNCH MENU', \
                                               command=self.see_lunchMenu, \
                                               bg='green', fg='white', \
                                               font='Helvetica 12 bold', \
                                               width=15, height=2)
            # Pack the lunch menu Button.
            self.lunch_button.pack(side='left')
    
            # ~~~~~~~~~~~~~~~~~~~~~~ Dinner Menu ~~~~~~~~~~~~~~~~~~~~~~~~
            self.dinner_button = tkinter.Button(self.bottom_frame, \
                                                text='DINNER MENU', \
                                                command=self.see_dinnerMenu, \
                                                bg='green', fg='white', \
                                                font='Helvetica 12 bold', \
                                                width=15, height=2)
            # Pack the lunch menu Button.
            self.dinner_button.pack(side='left')
    
            # ~~~~~~~~~~~~~~~~~~~~~~~ Desserts ~~~~~~~~~~~~~~~~~~~~~~~~~~
            self.dessert_button = tkinter.Button(self.bottom_frame, \
                                                 text='DESSERTS', \
                                                 command=self.see_desserts, \
                                                 bg='green', fg='white', \
                                                 font='Helvetica 12 bold', \
                                                 width=15, height=2)
            # Pack the lunch menu Button.
            self.dessert_button.pack(side='left')
    
            # ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            # Create the header of the reciept.
            # ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            print()
            print('----------------------------------')
            print('The Restaurant\n123 ABC Street')
            print('Houston, TX. 77000')
            print('----------------------------------')
            print()
            print('Item\t\t\tPrice')
            print('----------------------------------')
    
            # ---------------------------------------------------------------------------
            # Create a checkout Button.
            # ---------------------------------------------------------------------------
            self.checkout_button = tkinter.Button(self.top_frame, \
                                                  text='CHECKOUT', \
                                                  command=self.checkout, \
                                                  bg='red', fg='white', \
                                                  font='Helvetica 14 bold', \
                                                  width=15, height=2)
            # Pack the checkout Button.
            self.checkout_button.pack()
    
            # ---------------------------------------------------------------------------
            # Create a blank label for a space in
            # the top frame.
            # ---------------------------------------------------------------------------
            self.blankLabel_3 = tkinter.Label(self.top_frame)
    
            # Pack blankLabel_3.
            self.blankLabel_3.pack()
    
            # ---------------------------------------------------------------------------
            # Create a blank label for a space in
            # the image2_frame.
            # ---------------------------------------------------------------------------
            self.blankLabel_img2 = tkinter.Label(self.image2_frame)
    
            # Pack blankLabel_img2.
            self.blankLabel_img2.pack()
    
            # ---------------------------------------------------------------------------
            # Add PhotoImage widgets to the image2_frame.
            # ---------------------------------------------------------------------------
    
            # Coke image
            self.coke_photo = tkinter.PhotoImage(file='coke2.gif')
            self.img2_label1 = tkinter.Label(self.image2_frame, image=self.coke_photo).pack(side='left')
    
            # Bacon cheese burger image
            self.bcnburger_photo = tkinter.PhotoImage(file='bacon_burger2.gif')
            self.img2_label2 = tkinter.Label(self.image2_frame, image=self.bcnburger_photo).pack(side='left')
    
            # Chips & Salsa image
            self.salsa_photo = tkinter.PhotoImage(file='salsa2.gif')
            self.img2_label3 = tkinter.Label(self.image2_frame, image=self.salsa_photo).pack(side='left')
    
            # Steak image
            self.steak_photo = tkinter.PhotoImage(file='steak2.gif')
            self.img2_label4 = tkinter.Label(self.image2_frame, image=self.steak_photo).pack(side='left')
    
            # ---------------------------------------------------------------------------
            # Enter the tkinter main loop.
            # ---------------------------------------------------------------------------
            tkinter.mainloop()
    
        # *********************************************************************** ((( DRINKS ))) *****************************************************************************************
    
        # *******************************************************************************
        # The see_drinks method shows another
        # window that allows the user to choose
        # their drink of choice from a radiobutton
        # menu.
        # *******************************************************************************
        
        def see_drinks(self):
            # Create the drinks window.
            self.drinks = tkinter.Tk()
    
            # Create a title for the drinks menu.
            self.drinks.title('Drinks')
    
            # Resize the drinks window.
            self.drinks.geometry('500x400')
    
            # ---------------------------------------------------------------------------
            # Create three frames and pack them in.
            # ---------------------------------------------------------------------------
            self.top_frame = tkinter.Frame(self.drinks)
            self.middle_frame = tkinter.Frame(self.drinks)
            self.bottom_frame = tkinter.Frame(self.drinks)
            self.top_frame.pack()
            self.middle_frame.pack()
            self.bottom_frame.pack()
    
            # Create an IntVar object to use with
            # the Radiobuttons.
            self.radio_var = tkinter.StringVar()
    
            # Set the IntVar object equal to 1 in
            # order to have one Radiobutton
            # pre-selected.
            self.radio_var.set(1)
    
            # ---------------------------------------------------------------------------
            # Create a label widget containing
            # the text "CLICK A DRINK FOR MORE DETAILS & PRICES.".
            # ---------------------------------------------------------------------------
            self.label_3 = tkinter.Label(self.top_frame, \
                                         text='CLICK A DRINK FOR MORE DETAILS\n& PRICES.', \
                                         bg='red', fg='white', \
                                         font='Helvetica 12 bold')
            # Pack label_3.
            self.label_3.pack()
    
            # ---------------------------------------------------------------------------
            # Create a blank label for a space in
            # the top frame.
            # ---------------------------------------------------------------------------
            self.blankLabel_4 = tkinter.Label(self.top_frame)
    
            # Pack blankLabel_4.
            self.blankLabel_4.pack()
    
            # ---------------------------------------------------------------------------
            # Create the Radiobutton widgets for drink
            # choices and regular Buttons for drink
            # details and prices (all in top frame).
            # ---------------------------------------------------------------------------
    
            # ~~~~~~~~~~~~~~~~~~~~~~~ Regular Buttons ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            # Water Button
            self.water_button = tkinter.Button(self.top_frame, \
                                                text='Water', \
                                                command=self.drinkWater)
            # Dr. Pepper Button
            self.dp_button = tkinter.Button(self.top_frame, \
                                                text='Dr. Pepper', \
                                                command=self.drinkDP)
            # Coca Cola Button
            self.coke_button = tkinter.Button(self.top_frame, \
                                                text='Coca Cola', \
                                                command=self.drinkCoke)
            # Root Beer Button
            self.rb_button = tkinter.Button(self.top_frame, \
                                                text='Root Beer', \
                                                command=self.drinkRB)
            # Iced Tea Button
            self.tea_button = tkinter.Button(self.top_frame, \
                                                text='Iced Tea', \
                                                command=self.drinkTea)
            # Pack the Buttons.
            self.water_button.pack(side='left')
            self.dp_button.pack(side='left')
            self.coke_button.pack(side='left')
            self.rb_button.pack(side='left')
            self.tea_button.pack(side='left')
    
            # ---------------------------------------------------------------------------
            # Create a blank label for a space in
            # the middle frame.
            # ---------------------------------------------------------------------------
            self.blankLabel_5 = tkinter.Label(self.middle_frame, \
                                text='-----------------------------------------------', \
                                fg='black')
    
            # Pack blankLabel_5.
            self.blankLabel_5.pack()
            
            # ~~~~~~~~~~~~~~~~~~~~~~~ Radio Buttons ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            self.rb1 = tkinter.Radiobutton(self.middle_frame, \
                                           text='Water', command=self.drnk_option1, \
                                           value = 1)
            self.rb1.select()   # Initially select rb1
            
            self.rb2 = tkinter.Radiobutton(self.middle_frame, \
                                           text='Dr. Pepper', command=self.drnk_option2, \
                                           value = 2)
            self.rb2.deselect() # Initially deselect rb2
            
            self.rb3 = tkinter.Radiobutton(self.middle_frame, \
                                           text='Coca Cola', command=self.drnk_option3, \
                                           value = 3)
            self.rb3.deselect() # Initially deselect rb3
            
            self.rb4 = tkinter.Radiobutton(self.middle_frame, \
                                           text='Root Beer', command=self.drnk_option4, \
                                           value = 4)
            self.rb4.deselect() # Initially deselect rb4
            
            self.rb5 = tkinter.Radiobutton(self.middle_frame, \
                                           text='Iced Tea', command=self.drnk_option5, \
                                           value = 5)
            self.rb5.deselect() # Initially deselect rb5
            
            # Pack the Radiobuttons.
            self.rb1.pack()
            self.rb2.pack()
            self.rb3.pack()
            self.rb4.pack()
            self.rb5.pack()
    
            # ---------------------------------------------------------------------------
            # Create an OK button and a Cancel
            # button.
            # ---------------------------------------------------------------------------
            self.ok_button = tkinter.Button(self.bottom_frame, \
                                            text='   OK   ', command=self.show_drinkChoice)
            self.cancel_button = tkinter.Button(self.bottom_frame, \
                                              text='Cancel', command=self.drinks.destroy)
            # Pack the Buttons.
            self.ok_button.pack(side='left')
            self.cancel_button.pack(side='left')
    
        # *******************************************************************************
        # The following drink methods show details
        # of a chosen drink from the see_drinks function
        # when the user clicks a regular button for details.
        # *******************************************************************************
        
        def drinkWater(self):
            # Display an info dialog box about the water.
            tkinter.messagebox.showinfo('Water', \
                                        self.drink_items['H2O'])
    
        def drinkDP(self):
            # Display an info dialog box about the soda.
            tkinter.messagebox.showinfo('Dr. Pepper', \
                                        self.drink_items['DP'])
    
        def drinkCoke(self):
            # Display an info dialog box about the soda.
            tkinter.messagebox.showinfo('Coca Cola', \
                                        self.drink_items['Coke'])
            
        def drinkRB(self):
            # Display an info dialog box about the soda.
            tkinter.messagebox.showinfo('Root Beer', \
                                        self.drink_items['RB'])
    
        def drinkTea(self):
            # Display an info dialog box about the tea.
            tkinter.messagebox.showinfo('Iced Tea', \
                                        self.drink_items['Tea'])
    
        # *******************************************************************************
        # The see_drinkChoice method shows the choice
        # made by the user.
        # *******************************************************************************
        
        def show_drinkChoice(self):
            if self.flag_1 == 1:
                self.water = 0
                self.price += self.water
                print('Water\t\t\t$', format(self.water, '.2f'))
                self.drinks.destroy()
                
            elif self.flag_1 == 2:
                self.pepper = 0.99
                self.price += self.pepper
                print('Dr. Pepper\t\t$', format(self.pepper, '.2f'))
                self.drinks.destroy()
    
            elif self.flag_1 == 3:
                self.coke = 0.99
                self.price += self.coke
                print('Coca Cola\t\t$', format(self.coke, '.2f'))
                self.drinks.destroy()
    
            elif self.flag_1 == 4:
                self.rBeer = 0.99
                self.price += self.rBeer
                print('Root Beer\t\t$', format(self.rBeer, '.2f'))
                self.drinks.destroy()
    
            elif self.flag_1 == 5:
                self.tea = 0.89
                self.price += self.tea
                print('Iced Tea\t\t$', format(self.tea, '.2f'))
                self.drinks.destroy()
    
            else:
                self.none = 0
                self.price += self.none
                print('Water\t\t\t$', format(self.none, '.2f'))
                self.drinks.destroy()
    
        # *******************************************************************************
        # The following drnk_option methods are for
        # the selected Radiobutton made by the user
        # for their drink and flags a value to
        # obtain their choice.
        # *******************************************************************************
        
        def drnk_option1(self):
            self.flag_1 = 1
            
        def drnk_option2(self):
            self.flag_1 = 2
            
        def drnk_option3(self):
            self.flag_1 = 3
            
        def drnk_option4(self):
            self.flag_1 = 4
            
        def drnk_option5(self):
            self.flag_1 = 5
    
        # *********************************************************************** ((( APPETIZERS ))) **************************************************************************************
    
        # *******************************************************************************
        # The see_appetizers method shows another
        # window that allows the user to choose
        # their appetizer from a checkbox menu.
        # *******************************************************************************
        
        def see_appetizers(self):
            # Create the appetizers window.
            self.appetizers = tkinter.Tk()
    
            # Create a title for the appetizers menu.
            self.appetizers.title('Appetizers')
    
            # Resize the appetizers window.
            self.appetizers.geometry('500x400')
    
            # ---------------------------------------------------------------------------
            # Create five IntVar objects to use
            # with the Checkbuttons.
            # ---------------------------------------------------------------------------
            self.cb_var1 = tkinter.IntVar()
            self.cb_var2 = tkinter.IntVar()
            self.cb_var3 = tkinter.IntVar()
            self.cb_var4 = tkinter.IntVar()
            self.cb_var5 = tkinter.IntVar()
    
            # Set the IntVar objects to 0 "no checked boxes".
            self.cb_var1.set(0)
            self.cb_var2.set(0)
            self.cb_var3.set(0)
            self.cb_var4.set(0)
            self.cb_var5.set(0)
    
            # ---------------------------------------------------------------------------
            # Create the Checkbutton widgets
            # in the appetizers window.
            # ---------------------------------------------------------------------------
            self.cb1 = tkinter.Checkbutton(self.appetizers, \
                                           text='Chips & Salsa', \
                                           variable=self.cb_var1, \
                                           command=self.appet_option1).place(x=200, y=5)
            self.cb2 = tkinter.Checkbutton(self.appetizers, \
                                           text='Spinach Dip & Saltines', \
                                           variable=self.cb_var2, \
                                           command=self.appet_option2).place(x=200, y=25)
            self.cb3 = tkinter.Checkbutton(self.appetizers, \
                                           text='Classic Nachos', \
                                           variable=self.cb_var3, \
                                           command=self.appet_option3).place(x=200, y=45)
            self.cb4 = tkinter.Checkbutton(self.appetizers, \
                                           text='Spicy Buffalo Wings', \
                                           variable=self.cb_var4, \
                                           command=self.appet_option4).place(x=200, y=65)
            self.cb5 = tkinter.Checkbutton(self.appetizers, \
                                           text='Onion Rings', \
                                           variable=self.cb_var5, \
                                           command=self.appet_option5).place(x=200, y=85)
    
            # ---------------------------------------------------------------------------
            # Create the regular Button widgets to
            # see appetizer details and prices.
            # ---------------------------------------------------------------------------
            
            # ~~~~~~~~~~~~~~~~~~~~~~~ Regular Buttons ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            # Chips & Salsa Button
            self.salsa_button = tkinter.Button(self.appetizers, \
                                                text='Chips & Salsa', \
                                                command=self.appetSalsa)
            # Spinach Dip Button
            self.spinach_button = tkinter.Button(self.appetizers, \
                                                text='Spinach Dip & Saltines', \
                                                command=self.appetSpinDip)
            # Nachos Button
            self.nachos_button = tkinter.Button(self.appetizers, \
                                                text='Classic Nachos', \
                                                command=self.appetNachos)
            # Wings Button
            self.wings_button = tkinter.Button(self.appetizers, \
                                                text='Spicy Buffalo Wings', \
                                                command=self.appetWings)
            # Onion Rings Button
            self.orings_button = tkinter.Button(self.appetizers, \
                                                text='Onion Rings', \
                                                command=self.appetORings)
            # Pack the Buttons.
            self.salsa_button.pack(side='left')
            self.spinach_button.pack(side='left')
            self.nachos_button.pack(side='left')
            self.wings_button.pack(side='left')
            self.orings_button.pack(side='left')
    
            # ---------------------------------------------------------------------------
            # Create a blank label for a space in
            # the middle frame.
            # ---------------------------------------------------------------------------
            self.blankLabel_6 = tkinter.Label(self.appetizers, \
                                text='-----------------------------------------------', \
                                fg='black').place(x=135, y=135)
    
            # ---------------------------------------------------------------------------
            # Create a label widget containing
            # the text "CLICK ON AN APPETIZER FOR MORE DETAILS"
            # ---------------------------------------------------------------------------
            self.label_4 = tkinter.Label(self.appetizers, \
                                text='CLICK ON AN APPETIZER FOR MORE DETAILS', \
                                bg='dark green', fg='white', \
                                font='Helvetica 12 bold').place(x=70, y=155)
            
            # ---------------------------------------------------------------------------
            # Create an OK button and a Cancel Button.
            # ---------------------------------------------------------------------------
            self.ok_button = tkinter.Button(self.appetizers, \
                                            text='   OK   ', command=self.show_appetChoice).place(x=205, y=250)
            self.cancel_button = tkinter.Button(self.appetizers, \
                                                text='Cancel', command=self.appetizers.destroy).place(x=251, y=250)
    
        # *******************************************************************************
        # The following appet methods show details
        # of a chosen appetizers from the see_appetizers
        # function when the user clicks a regular button
        # for details.
        # *******************************************************************************
        
        def appetSalsa(self):
            # Display an info dialog box about the chips & salsa.
            tkinter.messagebox.showinfo('Chips & Salsa', \
                                        self.appet_items['Salsa'])
    
        def appetSpinDip(self):
            # Display an info dialog box about the spinach dip.
            tkinter.messagebox.showinfo('Spinach Dip & Saltines', \
                                        self.appet_items['SpinDip'])
    
        def appetNachos(self):
            # Display an info dialog box about the nachos.
            tkinter.messagebox.showinfo('Classic Nachos', \
                                        self.appet_items['Nachos'])
            
        def appetWings(self):
            # Display an info dialog box about the buffalo wings.
            tkinter.messagebox.showinfo('Spicy Buffalo Wings', \
                                        self.appet_items['Wings'])
    
        def appetORings(self):
            # Display an info dialog box about the onion rings.
            tkinter.messagebox.showinfo('Onion Rings', \
                                        self.appet_items['ORings'])
    
        # *******************************************************************************
        # The see_appetChoice method shows the choice
        # made by the user.
        # *******************************************************************************
        
        def show_appetChoice(self):
                if self.flag_2_1 == 1:
                    self.salsa = 1.00
                    self.price += self.salsa    
                    self.flag_2_1 = 0
                    print('Chips & Salsa\t\t$', format(self.salsa, '.2f'))
                    
                if self.flag_2_2 == 2:
                    self.spindip = 1.50
                    self.price += self.spindip
                    self.flag_2_2 = 0
                    print('Spinach Dip\t\t$', format(self.spindip, '.2f'))
    
                if self.flag_2_3 == 3:
                    self.nachos = 1.00
                    self.price += self.nachos
                    self.flag_2_3 = 0
                    print('Nachos\t\t\t$', format(self.nachos, '.2f'))
    
                if self.flag_2_4 == 4:
                    self.wings = 2.50
                    self.price += self.wings
                    self.flag_2_4 = 0
                    print('Buffalo Wings\t\t$', format(self.wings, '.2f'))
    
                if self.flag_2_5 == 5: 
                    self.orings = 1.75
                    self.price += self.orings
                    self.flag_2_5 = 0
                    print('Onion Rings\t\t$', format(self.orings, '.2f'))
    
                self.appetizers.destroy()
    
        # *******************************************************************************
        # The following appet_option methods are for
        # the selected Checkbutton made by the user
        # for their appetizer(s) and flags a value to
        # obtain their choice.
        # *******************************************************************************
        
        def appet_option1(self):
            self.flag_2_1 = 1   # Set the flag (flag the users choice) 
            self.cb_var1.set(1) # set the checkbutton equal to 1 showing " box checked"
            
        def appet_option2(self):
            self.flag_2_2 = 2   # Set the flag (flag the users choice)
            self.cb_var2.set(1) # set the checkbutton equal to 1 showing " box checked"
            
        def appet_option3(self):
            self.flag_2_3 = 3   # Set the flag (flag the users choice)
            self.cb_var3.set(1) # set the checkbutton equal to 1 showing " box checked"
            
        def appet_option4(self):
            self.flag_2_4 = 4   # Set the flag (flag the users choice)
            self.cb_var4.set(1) # set the checkbutton equal to 1 showing " box checked"
            
        def appet_option5(self):
            self.flag_2_5 = 5   # Set the flag (flag the users choice)
            self.cb_var5.set(1) # set the checkbutton equal to 1 showing " box checked"
    
        # *********************************************************************** ((( LUNCH MENU ))) **************************************************************************************
    
        # *******************************************************************************
        # The see_lunchMenu method shows another
        # window that allows the user to choose
        # their lunch from a radiobutton menu.
        # *******************************************************************************
        
        def see_lunchMenu(self):
            # Create the lunch window.
            self.lunch = tkinter.Tk()
    
            # Create a title for the lunch menu.
            self.lunch.title('Lunch')
    
            # Resize the lunch window.
            self.lunch.geometry('600x400')
    
            # ---------------------------------------------------------------------------
            # Create three frames and pack them in.
            # ---------------------------------------------------------------------------
            self.top_frame = tkinter.Frame(self.lunch)
            self.middle_frame = tkinter.Frame(self.lunch)
            self.bottom_frame = tkinter.Frame(self.lunch)
            self.top_frame.pack()
            self.middle_frame.pack()
            self.bottom_frame.pack()
    
            # Create an StringVar object to use with
            # the Radiobuttons.
            self.radio_var2 = tkinter.StringVar()
    
            # Set the StringVar object equal to 1 in
            # order to have one Radiobutton
            # pre-selected.
            self.radio_var2.set(1)
    
            # ---------------------------------------------------------------------------
            # Create a label widget containing
            # the text "CLICK A LUNCH ITEM FOR MORE DETAILS & PRICES.".
            # ---------------------------------------------------------------------------
            self.label_5 = tkinter.Label(self.top_frame, \
                                         text='CLICK A LUNCH ITEM FOR MORE DETAILS & PRICES', \
                                         bg='red', fg='white', \
                                         font='Helvetica 12 bold')
            # Pack label_5.
            self.label_5.pack()
    
            # ---------------------------------------------------------------------------
            # Create a blank label for a space in
            # the top frame.
            # ---------------------------------------------------------------------------
            self.blankLabel_7 = tkinter.Label(self.top_frame)
    
            # Pack blankLabel_7.
            self.blankLabel_7.pack()
    
            # ---------------------------------------------------------------------------
            # Create the Radiobutton widgets in
            # the top frame for lunch item choices
            # and regular Buttons for lunch item
            # details and prices in the top frame.
            # ---------------------------------------------------------------------------
    
            # ~~~~~~~~~~~~~~~~~~~~~~~~~~ Regualr Buttons ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            # Cheese Burger Button
            self.chseBurg_button = tkinter.Button(self.top_frame, \
                                                  text='Cheese Burger', \
                                                  command=self.lunchBurger1)
            # Bacon Cheese Burger Button
            self.bcnChseBurg_button = tkinter.Button(self.top_frame, \
                                                     text='Bacon Cheese Burger', \
                                                     command=self.lunchBurger2)
            # Grilled Chicken Button
            self.chicken_button = tkinter.Button(self.top_frame, \
                                                text='Grilled Chicken', \
                                                command=self.lunchChicken)
            # BLT Button
            self.blt_button = tkinter.Button(self.top_frame, \
                                                text='BLT Sandwich', \
                                                command=self.lunchBLT)
            # Soup & Salad Button
            self.ss_button = tkinter.Button(self.top_frame, \
                                                text='Soup & Salad', \
                                                command=self.lunchSoup)
            # Pack the Buttons.
            self.chseBurg_button.pack(side='left')
            self.bcnChseBurg_button.pack(side='left')
            self.chicken_button.pack(side='left')
            self.blt_button.pack(side='left')
            self.ss_button.pack(side='left')
    
            # ---------------------------------------------------------------------------
            # Create a blank label for a space in
            # the middle frame.
            # ---------------------------------------------------------------------------
            self.blankLabel_8 = tkinter.Label(self.middle_frame, \
                                text='-----------------------------------------------', \
                                fg='black')
    
            # Pack blankLabel_8.
            self.blankLabel_8.pack()
    
            # ~~~~~~~~~~~~~~~~~~~~~~~~~~~ Radio Buttons ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    
            # Need a blank RadioButton(radbBlank) that is "pre-selected" to allow 
            # all the other Radiobuttons to be deselected. This blank Radiobutton
            # does not show in the lunch menu window.
            
            self.radbBlank = tkinter.Radiobutton(self.middle_frame, \
                                                 value = 0)
            self.radbBlank.select()     # Initially select radbBlank
            
            self.radb1 = tkinter.Radiobutton(self.middle_frame, \
                                             text='Cheese Burger', command=self.lunch_option1, \
                                             value = 1)
            self.radb1.deselect()     # Initially deselect radb1
    
            self.radb2 = tkinter.Radiobutton(self.middle_frame, \
                                             text='Bacon Cheese Burger', command=self.lunch_option2, \
                                             value = 2)
            self.radb2.deselect()   # Initially deselect radb2
    
            self.radb3 = tkinter.Radiobutton(self.middle_frame, \
                                             text='Grilled Chicken', command=self.lunch_option3, \
                                             value = 3)
            self.radb3.deselect()     # Initially deselect radb3
    
            self.radb4 = tkinter.Radiobutton(self.middle_frame, \
                                             text='BLT Sandwich', command=self.lunch_option4, \
                                             value = 4)
            self.radb4.deselect()     # Initially deselect radb4
    
            self.radb5 = tkinter.Radiobutton(self.middle_frame, \
                                             text='Soup & Salad', command=self.lunch_option5, \
                                             value = 5)
            self.radb5.deselect()     # Initially deselect radb5
    
            # Pack the Radiobuttons.
            self.radb1.pack()
            self.radb2.pack()
            self.radb3.pack()
            self.radb4.pack()
            self.radb5.pack()
    
            # ---------------------------------------------------------------------------
            # Create an OK button and a Cancel
            # button.
            # ---------------------------------------------------------------------------
            self.ok_button = tkinter.Button(self.bottom_frame, \
                                            text='   OK   ', command=self.show_lunchChoice)
            self.cancel_button = tkinter.Button(self.bottom_frame, \
                                              text='Cancel', command=self.lunch.destroy)
            # Pack the Buttons.
            self.ok_button.pack(side='left')
            self.cancel_button.pack(side='left')
    
        # *******************************************************************************
        # The following lunch methods show details
        # of a chosen lunch item from the see_lunchMenu
        # function when the user clicks a regular button
        # for details.
        # *******************************************************************************
        
        def lunchBurger1(self):
            # Display an info dialog box about the cheese burger.
            tkinter.messagebox.showinfo('Cheese Burger', \
                                        self.lunch_items['Burg1'])
    
        def lunchBurger2(self):
            # Display an info dialog box about the bacon cheese burger.
            tkinter.messagebox.showinfo('Bacon Cheese Burger', \
                                        self.lunch_items['Burg2'])
    
        def lunchChicken(self):
            # Display an info dialog box about the grilled chicken.
            tkinter.messagebox.showinfo('Grilled Chicken', \
                                        self.lunch_items['GrldChkn'])
            
        def lunchBLT(self):
            # Display an info dialog box about the BLT sandwich.
            tkinter.messagebox.showinfo('BLT Sandwich', \
                                        self.lunch_items['BLT'])
    
        def lunchSoup(self):
            # Display an info dialog box about the soup and salad.
            tkinter.messagebox.showinfo('Soup & Salad', \
                                        self.lunch_items['SS'])
    
        # *******************************************************************************
        # The see_lunchChoice method shows the
        # choice made by the user.
        # *******************************************************************************
        
        def show_lunchChoice(self):
            if self.flag_3 == 1:
                self.burger1 = 3.25
                self.price += self.burger1
                print('Chse Burger\t\t$', format(self.burger1, '.2f'))
                self.lunch.destroy()
                
            elif self.flag_3 == 2:
                self.burger2 = 3.50
                self.price += self.burger2
                print('Bcn Chse Burg\t\t$', format(self.burger2, '.2f'))
                self.lunch.destroy()
    
            elif self.flag_3 == 3:
                self.grldCkn = 4.00
                self.price += self.grldCkn
                print('Grld Chicken\t\t$', format(self.grldCkn, '.2f'))
                self.lunch.destroy()
    
            elif self.flag_3 == 4:
                self.blt = 3.00
                self.price += self.blt
                print('BLT Sndwch\t\t$', format(self.blt, '.2f'))
                self.lunch.destroy()
    
            elif self.flag_3 == 5:
                self.ss = 2.65
                self.price += self.ss
                print('Soup & Salad\t\t$', format(self.ss, '.2f'))
                self.lunch.destroy()
    
            else:
                self.none = 0
                self.price += self.none
                print('No Lunch Item\t\t$', format(self.none, '.2f'))
                self.lunch.destroy()
    
        # *******************************************************************************
        # The following lunch option methods are for
        # the selected Radiobutton made by the user
        # for their lunch and flags a value to
        # obtain their choice.
        # *******************************************************************************
        
        def lunch_option1(self):
            self.flag_3 = 1
            
        def lunch_option2(self):
            self.flag_3 = 2
            
        def lunch_option3(self):
            self.flag_3 = 3
            
        def lunch_option4(self):
            self.flag_3 = 4
            
        def lunch_option5(self):
            self.flag_3 = 5
    
        # *********************************************************************** ((( DINNER MENU ))) *************************************************************************************
    
        # *******************************************************************************
        # The see_dinnerMenu method shows another
        # window that allows the user to choose
        # their dinner from a checkbox menu.
        # *******************************************************************************
        
        def see_dinnerMenu(self):
            # Create the dinner window.
            self.dinner = tkinter.Tk()
    
            # Create a title for the dinner menu.
            self.dinner.title('Dinner')
    
            # Resize the dinner window.
            self.dinner.geometry('600x400')
    
            # ---------------------------------------------------------------------------
            # Create three frames and pack them in.
            # ---------------------------------------------------------------------------
            self.top_frame = tkinter.Frame(self.dinner)
            self.middle_frame = tkinter.Frame(self.dinner)
            self.bottom_frame = tkinter.Frame(self.dinner)
            self.top_frame.pack()
            self.middle_frame.pack()
            self.bottom_frame.pack()
    
            # Create an StringVar object to use with
            # the Radiobuttons.
            self.radio_var3 = tkinter.StringVar()
    
            # Set the StringVar object equal to 1 in
            # order to have one Radiobutton
            # pre-selected.
            self.radio_var3.set(1)
    
            # ---------------------------------------------------------------------------
            # Create a label widget containing
            # the text "CLICK A DINNER ITEM FOR MORE DETAILS & PRICES.".
            # ---------------------------------------------------------------------------
            self.label_6 = tkinter.Label(self.top_frame, \
                                         text='CLICK A DINNER ITEM FOR MORE DETAILS & PRICES', \
                                         bg='red', fg='white', \
                                         font='Helvetica 12 bold')
            # Pack label_6.
            self.label_6.pack()
    
            # ---------------------------------------------------------------------------
            # Create a blank label for a space in
            # the top frame.
            # ---------------------------------------------------------------------------
            self.blankLabel_8 = tkinter.Label(self.top_frame)
    
            # Pack blankLabel_8.
            self.blankLabel_8.pack()
    
            # ---------------------------------------------------------------------------
            # Create the Radiobutton widgets in
            # the top frame for dinner item choices
            # and regular Buttons for dinner item
            # details and prices in the top frame.
            # ---------------------------------------------------------------------------
    
            # ~~~~~~~~~~~~~~~~~~~~~~~~~~ Regualr Buttons ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            # Steak Button
            self.steak_button = tkinter.Button(self.top_frame, \
                                               text='Ribeye Steak', \
                                               command=self.dinnerSteak)
            # Quesadillas Button
            self.quesadilla_button = tkinter.Button(self.top_frame, \
                                                    text='Quesadillas', \
                                                    command=self.dinnerQuesadilla)
            # Chicken Salad Button
            self.chickenS_button = tkinter.Button(self.top_frame, \
                                                  text='Chicken Salad', \
                                                  command=self.dinnerChickenS)
            # Crawfish Button
            self.crawfish_button = tkinter.Button(self.top_frame, \
                                                  text='Boiled Crawfish', \
                                                  command=self.dinnerCrawfish)
            # The Restaurant Burger Button
            self.restBurger_button = tkinter.Button(self.top_frame, \
                                                    text='Restaurant Burger', \
                                                    command=self.dinnerRestBurger)
            # Pack the Buttons.
            self.steak_button.pack(side='left')
            self.quesadilla_button.pack(side='left')
            self.chickenS_button.pack(side='left')
            self.crawfish_button.pack(side='left')
            self.restBurger_button.pack(side='left')
    
            # ---------------------------------------------------------------------------
            # Create a blank label for a space in
            # the middle frame.
            # ---------------------------------------------------------------------------
            self.blankLabel_9 = tkinter.Label(self.middle_frame, \
                                text='-----------------------------------------------', \
                                fg='black')
    
            # Pack blankLabel_9.
            self.blankLabel_9.pack()
    
            # ~~~~~~~~~~~~~~~~~~~~~~~~~~~ Radio Buttons ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    
            # Need a blank RadioButton(radbBlank) that is "pre-selected" to allow 
            # all the other Radiobuttons to be deselected. This blank Radiobutton
            # does not show in the dinner menu window.
            self.radbBlank2 = tkinter.Radiobutton(self.middle_frame, \
                                                  value = 0)
            self.radbBlank2.select()     # Initially select radbBlank
            
            self.radb1 = tkinter.Radiobutton(self.middle_frame, \
                                             text='Steak', command=self.dinner_option1, \
                                             value = 1)
            self.radb1.deselect()     # Initially deselect radb1
    
            self.radb2 = tkinter.Radiobutton(self.middle_frame, \
                                             text='Quesadillas', command=self.dinner_option2, \
                                             value = 2)
            self.radb2.deselect()   # Initially deselect radb2
    
            self.radb3 = tkinter.Radiobutton(self.middle_frame, \
                                             text='Chicken Salad', command=self.dinner_option3, \
                                             value = 3)
            self.radb3.deselect()     # Initially deselect radb3
    
            self.radb4 = tkinter.Radiobutton(self.middle_frame, \
                                             text='Crawfish', command=self.dinner_option4, \
                                             value = 4)
            self.radb4.deselect()     # Initially deselect radb4
    
            self.radb5 = tkinter.Radiobutton(self.middle_frame, \
                                             text='The Restaurant Burger', command=self.dinner_option5, \
                                             value = 5)
            self.radb5.deselect()     # Initially deselect radb5
    
            # Pack the Radiobuttons.
            self.radb1.pack()
            self.radb2.pack()
            self.radb3.pack()
            self.radb4.pack()
            self.radb5.pack()
    
            # ---------------------------------------------------------------------------
            # Create an OK button and a Cancel
            # button.
            # ---------------------------------------------------------------------------
            self.ok_button = tkinter.Button(self.bottom_frame, \
                                            text='   OK   ', command=self.show_dinnerChoice)
            self.cancel_button = tkinter.Button(self.bottom_frame, \
                                              text='Cancel', command=self.dinner.destroy)
            # Pack the Buttons.
            self.ok_button.pack(side='left')
            self.cancel_button.pack(side='left')
    
        # *******************************************************************************
        # The following dinner methods show details
        # of a chosen dinner item from the see_dinnerMenu
        # function when the user clicks a regular button
        # for details.
        # *******************************************************************************
        
        def dinnerSteak(self):
            # Display an info dialog box about the steak.
            tkinter.messagebox.showinfo('Ribeye Steak', \
                                        self.dinner_items['Steak'])
    
        def dinnerQuesadilla(self):
            # Display an info dialog box about the quesadillas.
            tkinter.messagebox.showinfo('Quesadillas', \
                                        self.dinner_items['Quesadillas'])
    
        def dinnerChickenS(self):
            # Display an info dialog box about the chicken salad.
            tkinter.messagebox.showinfo('Chicken Salad', \
                                        self.dinner_items['Chicken Salad'])
            
        def dinnerCrawfish(self):
            # Display an info dialog box about the crawfish.
            tkinter.messagebox.showinfo('Crawfish', \
                                        self.dinner_items['Crawfish'])
    
        def dinnerRestBurger(self):
            # Display an info dialog box about The Restaurant Burger.
            tkinter.messagebox.showinfo('The Restaurant Burger', \
                                        self.dinner_items['The Restaurant Burger'])
    
        # *******************************************************************************
        # The see_dinnerChoice method shows the
        # choice made by the user.
        # *******************************************************************************
        
        def show_dinnerChoice(self):
            if self.flag_4 == 1:
                self.steak = 8.50
                self.price += self.steak
                print('Steak\t\t\t$', format(self.steak, '.2f'))
                self.dinner.destroy()
                
            elif self.flag_4 == 2:
                self.quesadilla = 4.75
                self.price += self.quesadilla
                print('Quesadillas\t\t$', format(self.quesadilla, '.2f'))
                self.dinner.destroy()
    
            elif self.flag_4 == 3:
                self.chickenS = 4.00
                self.price += self.chickenS
                print('Chkn Salad\t\t$', format(self.chickenS, '.2f'))
                self.dinner.destroy()
    
            elif self.flag_4 == 4:
                self.crawfish = 18.00
                self.price += self.crawfish
                print('Crawfish\t\t$', format(self.crawfish, '.2f'))
                self.dinner.destroy()
    
            elif self.flag_4 == 5:
                self.restBurger = 4.00
                self.price += self.restBurger
                print('Rest Burger\t\t$', format(self.restBurger, '.2f'))
                self.dinner.destroy()
    
            else:
                self.none = 0
                self.price += self.none
                print('No Dinner Item\t\t$', format(self.none, '.2f'))
                self.dinner.destroy()
    
        # *******************************************************************************
        # The following dinner option methods are for
        # the selected Radiobutton made by the user
        # for their dinner and flags a value to
        # obtain their choice.
        # *******************************************************************************
        
        def dinner_option1(self):
            self.flag_4 = 1
            
        def dinner_option2(self):
            self.flag_4 = 2
            
        def dinner_option3(self):
            self.flag_4 = 3
            
        def dinner_option4(self):
            self.flag_4 = 4
            
        def dinner_option5(self):
            self.flag_4 = 5
    
        # *********************************************************************** ((( DESSERTS ))) ****************************************************************************************
    
        # *******************************************************************************
        # The see_desserts method shows another
        # window that allows the user to choose
        # their dessert from a checkbox menu.
        # *******************************************************************************
        
        def see_desserts(self):
            # Create the desserts window.
            self.desserts = tkinter.Tk()
    
            # Create a title for the desserts menu.
            self.desserts.title('Desserts')
    
            # Resize the desserts window.
            self.desserts.geometry('600x400')
    
            # ---------------------------------------------------------------------------
            # Create three frames and pack them in.
            # ---------------------------------------------------------------------------
            self.top_frame = tkinter.Frame(self.desserts)
            self.middle_frame = tkinter.Frame(self.desserts)
            self.bottom_frame = tkinter.Frame(self.desserts)
            self.top_frame.pack()
            self.middle_frame.pack()
            self.bottom_frame.pack()
    
            # Create an StringVar object to use with
            # the Radiobuttons.
            self.radio_var4 = tkinter.StringVar()
    
            # Set the StringVar object equal to 1 in
            # order to have one Radiobutton
            # pre-selected.
            self.radio_var4.set(1)
    
            # ---------------------------------------------------------------------------
            # Create a label widget containing
            # the text "CLICK A DESSERT ITEM FOR MORE DETAILS & PRICES.".
            # ---------------------------------------------------------------------------
            self.label_7 = tkinter.Label(self.top_frame, \
                                         text='CLICK A DESSERT ITEM FOR MORE DETAILS & PRICES', \
                                         bg='red', fg='white', \
                                         font='Helvetica 12 bold')
            # Pack label_7.
            self.label_7.pack()
    
            # ---------------------------------------------------------------------------
            # Create a blank label for a space in
            # the top frame.
            # ---------------------------------------------------------------------------
            self.blankLabel_9 = tkinter.Label(self.top_frame)
    
            # Pack blankLabel_9.
            self.blankLabel_9.pack()
    
            # ---------------------------------------------------------------------------
            # Create the Radiobutton widgets in
            # the top frame for dessert item choices
            # and regular Buttons for dessert item
            # details and prices in the top frame.
            # ---------------------------------------------------------------------------
    
            # ~~~~~~~~~~~~~~~~~~~~~~~~~~ Regualr Buttons ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            # Homemade Vanilla Ice Cream Button
            self.iceCream_button = tkinter.Button(self.top_frame, \
                                                  text='Vanilla Ice Cream', \
                                                  command=self.dessertIceCream)
            # Blueberry Cheesecake Button
            self.bbcCake_button = tkinter.Button(self.top_frame, \
                                                 text='Cheesecake', \
                                                 command=self.dessertBBCcake)
            # Chocolate Milkshake Button
            self.milkshake_button = tkinter.Button(self.top_frame, \
                                                   text='Chocolate Milkshake', \
                                                   command=self.dessertMilkshake)
            # Carrot Cake Button
            self.cake_button = tkinter.Button(self.top_frame, \
                                              text='Carrot Cake', \
                                              command=self.dessertCake)
            # Root Beer Float Button
            self.rbFloat_button = tkinter.Button(self.top_frame, \
                                                 text='Root Beer Float', \
                                                 command=self.dessertRBfloat)
            # Pack the Buttons.
            self.iceCream_button.pack(side='left')
            self.bbcCake_button.pack(side='left')
            self.milkshake_button.pack(side='left')
            self.cake_button.pack(side='left')
            self.rbFloat_button.pack(side='left')
    
            # ---------------------------------------------------------------------------
            # Create a blank label for a space in
            # the middle frame.
            # ---------------------------------------------------------------------------
            self.blankLabel_10 = tkinter.Label(self.middle_frame, \
                                 text='-----------------------------------------------', \
                                 fg='black')
    
            # Pack blankLabel_10.
            self.blankLabel_10.pack()
    
            # ~~~~~~~~~~~~~~~~~~~~~~~~~~~ Radio Buttons ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    
            # Need a blank RadioButton(radbBlank) that is "pre-selected" to allow 
            # all the other Radiobuttons to be deselected. This blank Radiobutton
            # does not show in the dessert menu window.
            
            self.radbBlank3 = tkinter.Radiobutton(self.middle_frame, \
                                                  value = 0)
            self.radbBlank3.select()     # Initially select radbBlank
            
            self.radb1 = tkinter.Radiobutton(self.middle_frame, \
                                             text='Ice Cream', command=self.dessert_option1, \
                                             value = 1)
            self.radb1.deselect()        # Initially deselect radb1
    
            self.radb2 = tkinter.Radiobutton(self.middle_frame, \
                                             text='Cheesecake', command=self.dessert_option2, \
                                             value = 2)
            self.radb2.deselect()        # Initially deselect radb2
    
            self.radb3 = tkinter.Radiobutton(self.middle_frame, \
                                             text='Milkshake', command=self.dessert_option3, \
                                             value = 3)
            self.radb3.deselect()       # Initially deselect radb3
    
            self.radb4 = tkinter.Radiobutton(self.middle_frame, \
                                             text='Carrot Cake', command=self.dessert_option4, \
                                             value = 4)
            self.radb4.deselect()       # Initially deselect radb4
    
            self.radb5 = tkinter.Radiobutton(self.middle_frame, \
                                             text='Root Beer Float', command=self.dessert_option5, \
                                             value = 5)
            self.radb5.deselect()       # Initially deselect radb5
    
            # Pack the Radiobuttons.
            self.radb1.pack()
            self.radb2.pack()
            self.radb3.pack()
            self.radb4.pack()
            self.radb5.pack()
    
            # ---------------------------------------------------------------------------
            # Create an OK button and a Cancel
            # button.
            # ---------------------------------------------------------------------------
            self.ok_button = tkinter.Button(self.bottom_frame, \
                                            text='   OK   ', command=self.show_dessertChoice)
            self.cancel_button = tkinter.Button(self.bottom_frame, \
                                              text='Cancel', command=self.desserts.destroy)
            # Pack the Buttons.
            self.ok_button.pack(side='left')
            self.cancel_button.pack(side='left')
    
        # *******************************************************************************
        # The following dessert methods show details
        # of a chosen dessert item from the see_dessertMenu
        # function when the user clicks a regular button
        # for details.
        # *******************************************************************************
        def dessertIceCream(self):
            # Display an info dialog box about the ice cream.
            tkinter.messagebox.showinfo('Homemade Vanilla Ice Cream', \
                                        self.dessert_items['Homemade Vanilla Ice Cream'])
    
        def dessertBBCcake(self):
            # Display an info dialog box about the blueberry cheesecake.
            tkinter.messagebox.showinfo('Blueberry Cheesecake', \
                                        self.dessert_items['Blueberry Cheesecake'])
    
        def dessertMilkshake(self):
            # Display an info dialog box about the chocolate milkshake.
            tkinter.messagebox.showinfo('Chocolate Milkshae', \
                                        self.dessert_items['Chocolate Milkshake'])
            
        def dessertCake(self):
            # Display an info dialog box about the carrot cake.
            tkinter.messagebox.showinfo('Carrot Cake', \
                                        self.dessert_items['Carrot Cake'])
    
        def dessertRBfloat(self):
            # Display an info dialog box about the root beer float.
            tkinter.messagebox.showinfo('Root Beer Float', \
                                        self.dessert_items['Root Beer Float'])
    
        # *******************************************************************************
        # The see_dessertChoice method shows the
        # choice made by the user.
        # *******************************************************************************
        def show_dessertChoice(self):
            if self.flag_5 == 1:
                self.iceCream = 1.50
                self.price += self.iceCream
                print('Ice Cream\t\t$', format(self.iceCream, '.2f'))
                self.desserts.destroy()
                
            elif self.flag_5 == 2:
                self.cheesecake = 2.00
                self.price += self.cheesecake
                print('Cheesecake\t\t$', format(self.cheesecake, '.2f'))
                self.desserts.destroy()
    
            elif self.flag_5 == 3:
                self.milkshake = 1.75
                self.price += self.milkshake
                print('Milkshake\t\t$', format(self.milkshake, '.2f'))
                self.desserts.destroy()
    
            elif self.flag_5 == 4:
                self.carrot = 2.00
                self.price += self.carrot
                print('Carrot Ck\t\t$', format(self.carrot, '.2f'))
                self.desserts.destroy()
    
            elif self.flag_5 == 5:
                self.rbFloat = 1.90
                self.price += self.rbFloat
                print('RB Float\t\t$', format(self.rbFloat, '.2f'))
                self.desserts.destroy()
    
            else:
                self.none = 0
                self.price += self.none
                print('No Dessert Item\t\t$', format(self.none, '.2f'))
                self.desserts.destroy()
    
        # *******************************************************************************
        # The following dessert option methods are for
        # the selected Radiobutton made by the user
        # for their dessert and flags a value to
        # obtain their choice.
        # *******************************************************************************
        def dessert_option1(self):
            self.flag_5 = 1
            
        def dessert_option2(self):
            self.flag_5 = 2
            
        def dessert_option3(self):
            self.flag_5 = 3
            
        def dessert_option4(self):
            self.flag_5 = 4
            
        def dessert_option5(self):
            self.flag_5 = 5
    
        # *********************************************************************** ((( CHECKOUT ))) ****************************************************************************************
    
        # *******************************************************************************
        # The checkout function gives the subtotal,
        # tax, and final total of the reciept and
        # at the bottom gives the date and time.
        # *******************************************************************************
        def checkout(self):
            self.main_window.destroy()
            self.subtotal = self.price
            self.tax = self.subtotal*0.0825
            self.total = self.subtotal+self.tax
            print('----------------------------------')
            print('Sub-total\t\t$', format(self.subtotal, '.2f'))
            print('Tax\t\t\t$', format(self.tax, '.2f'))
            print()
            print('Total\t\t\t$', format(self.total, '.2f'))
            print()
            print('----------------------------------')
            print('Time/Date: ', time.strftime('%H:%M:%S'), ' ', \
                  time.strftime('%m/%d/%Y'))
            print()
            print('*********** THANK YOU! ***********')
    
    
    # Create an instance of the MyGUI class.
    my_gui = MyGUI()
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

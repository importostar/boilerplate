---
title: answer_test_4
date: 2020-05-07
---
Example Python program answer_test_4.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import numpy as np
* from sklearn import linear_model

## Classes

* class MarketingCosts:

## Methods

* def desired_marketing_expenditure(marketing_expenditure, units_sold, desired_units_sold):

## Code

Python example

    import numpy as np
    from sklearn import linear_model
    
    class MarketingCosts:
    
        # param marketing_expenditure list. Expenditure for each previous campaign.
        # param units_sold list. The number of units sold for each previous campaign.
        # param desired_units_sold int. Target number of units to sell in the new campaign.
        # returns float. Required amount of money to be invested.
        @staticmethod
        def desired_marketing_expenditure(marketing_expenditure, units_sold, desired_units_sold):
            x = np.array(units_sold).reshape(-1,1)
            y = np.array(marketing_expenditure).reshape(-1,1)
            y_predict = np.array(desired_units_sold).reshape(-1, 1)
            
            reg = linear_model.TheilSenRegressor()
            reg.fit(x,y)
            
            desired_marketing_expenditure = reg.predict(y_predict)
            return float(desired_marketing_expenditure)
    
    
    #For example, with the parameters below the function should return 250000.0.
    print(MarketingCosts.desired_marketing_expenditure(
        [300000, 200000, 400000, 300000, 100000],
        [60000, 50000, 90000, 80000, 30000],
        60000))

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

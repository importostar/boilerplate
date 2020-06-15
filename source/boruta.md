---
title: boruta
date: 2020-05-07
---
Example Python program boruta.py

## Modules

* from sklearn.ensemble import RandomForestClassifier
* from boruta import BorutaPy

## Code

Python example

    from sklearn.ensemble import RandomForestClassifier
    from boruta import BorutaPy
    
    # load X and y
    # NOTE BorutaPy accepts numpy arrays only, hence the .values attribute
    X = new_test_data.values
    y = new_test_data['churn'].values
    
    
    # define random forest classifier, with utilising all cores and
    # sampling in proportion to y labels
    rf = RandomForestClassifier(n_jobs=-1, class_weight='balanced', max_depth=5)
    
    # define Boruta feature selection method
    feat_selector = BorutaPy(rf, n_estimators='auto', verbose=2, random_state=1)
    
    # find all relevant features - 5 features should be selected
    feat_selector.fit(X, y)
    
    # check selected features - first 5 features are selected
    feat_selector.support_
    
    # check ranking of features
    feat_selector.ranking_
    
    # call transform() on X to filter it down to selected features
    X_filtered = feat_selector.transform(X)
    
    # Identify which column names should be kept in the model
    new_features = new_test_data.iloc[:,feat_selector.support_].columns
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

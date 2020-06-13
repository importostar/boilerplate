---
title: xgb_py_snippets
date: 2020-05-07
---
Example Python program xgb_py_snippets.py

## Modules

* import xgboost as xgb
* bst.get_score(importance_type='gain')
* plot_importance(bst, max_num_features=30, ax = ax)

## Code

Python example

    import xgboost as xgb
    
    ## xgboost param docs 
    ## https://xgboost.readthedocs.io/en/latest/parameter.html
    
    ## xgboost example
    ## https://github.com/dmlc/xgboost/tree/master/demo
    
    
    
    
    ##### params setting
    xgb_params = {
      'objective': 'binary:logistic',
      ## reg:squarederror
      ## multi:softprob
      ## multi:softmax
      
      'max_depth': 6,
      'eta': 0.05,
      'gamma': 0.1,
      ## minimum loss reduction required
      
      'lambda': 0.5,
      ## L2 reg
      
      'alpha': 0.5,
      ## L1 reg 
      
      #'num_class':3, 
      ## For multi class
      
      #'n_estimators' : 100
      ## for sklearn api
       
      'tree_method': 'auto',
      
      'nthread': 10
      ## for limiting threads
    }
    
    
    ##### XGB train
    
    ## xgb api
    ## https://xgboost.readthedocs.io/en/latest/python/python_api.html
    
    ### python functional api
    train_set = xgb.DMatrix(train_X, train_y)
    bst = xgb.train(xgb_params, train_set, num_boost_round = 500)
    pred = bst.predict(xgb.DMatrix(test_y))
    
    ### scikit learn api
    clf = xgb.XGBClassifier(**xgb_params)
    clf.fit(X, y, eval_metric='auc')
    
    ### pred for binary classification
    np.where(pred > 0.5, 1, 0)
    
    
    ##### XGB CV
    
    
    ##### get feat imp
    bst.get_score(importance_type='gain')
    
    ##### feat imp plot 
    fig, ax = plt.subplots(1,1,figsize=(10, 10))
    plot_importance(bst, max_num_features=30, ax = ax)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: outliers
date: 2020-05-07
---
Example Python program outliers.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from collections import Counter

## Methods

* def detect_outliers(df,n,features):

## Code

Python example

    from collections import Counter
    # Outlier detection 
    def detect_outliers(df,n,features):
            '''
            df: dataset, pandas Dataframe format, 
            n: number of outliers, if a record has more than one feature value is a profit group point, then if the total number of these points is greater than N, then I think this record needs to be deleted, 
            feature: a collection of attribute values, that is, the column name of Dataframe, which returns the entire data set of the entry that needs to be deleted under Table index.
            '''
        outlier_indices = []
        for col in features:
            # 1st quartile (25%)
            Q1 = np.percentile(df[col],25)
            # 3rd quartile (75%)
            Q3 = np.percentile(df[col],75)
            # Interquartile range (IQR)
            IQR = Q3 - Q1
            # outlier step
            outlier_step = 1.5 * IQR
            # Determine a list of indices of outliers for feature col
            outlier_list_col = df[(df[col] < Q1 - outlier_step) | (df[col] > Q3 + outlier_step )].index       
            # append the found outlier indices for col to the list of outlier indices 
            outlier_indices.extend(outlier_list_col)
            
        # select observations containing more than n outliers
        outlier_indices = Counter(outlier_indices)        
        multiple_outliers = list( k for k, v in outlier_indices.items() if v >= n )
        return multiple_outliers 
        
    #-------------------------------------------------    
    # Identify and list the outliers that should be potentially dropped
    drop_outliers = detect_outliers(train_data,2, features)
    print("The dataset contains", len(drop_outliers),"outliers")
    train_data.loc[drop_outliers]
    
    
    # Removing outliers
    Q1 = train_data.quantile(0.25)
    Q3 = train_data.quantile(0.75)
    IQR = Q3 - Q1
    print('IQR das variáveis:\n')
    print(IQR)
    
    print()
    print('Dimensões do dataset com outliers:', train_data.shape)
    
    train_data = train_data[~((train_data < (Q1 - 1.5 * IQR)) |(train_data > (Q3 + 1.5 * IQR))).any(axis=1)]
    X = train_data[features]
    y = train_data[target]
    
    print('Dimensões do dataset sem outliers:', train_data.shape)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

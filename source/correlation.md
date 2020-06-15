---
title: correlation
date: 2020-05-07
---
Example Python program correlation.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Code

Python example

    # Find all correlations and sort 
    correlations_data = data.corr()['score'].sort_values()
    
    # Print the most negative correlations
    print(correlations_data.head(15), '\n')
    
    # Print the most positive correlations
    print(correlations_data.tail(15))
    
    #-------------
    
    # Select the numeric columns
    numeric_subset = data.select_dtypes('number')
    
    # Create columns with square root and log of numeric columns
    for col in numeric_subset.columns:
        # Skip the Energy Star Score column
        if col == 'score':
            next
        else:
            numeric_subset['sqrt_' + col] = np.sqrt(numeric_subset[col])
            numeric_subset['log_' + col] = np.log(numeric_subset[col])
    
    # Select the categorical columns
    categorical_subset = data[['Borough', 'Largest Property Use Type']]
    
    # One hot encode
    categorical_subset = pd.get_dummies(categorical_subset)
    
    # Join the two dataframes using concat
    # Make sure to use axis = 1 to perform a column bind
    features = pd.concat([numeric_subset, categorical_subset], axis = 1)
    
    # Drop buildings without an energy star score
    features = features.dropna(subset = ['score'])
    
    # Find correlations with the score 
    correlations = features.corr()['score'].dropna().sort_values()
    
    #----------------
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

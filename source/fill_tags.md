---
title: fill_tags
date: 2020-05-07
---
Example Python program fill_tags.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from time import time

## Methods

* def fill_tags(DF, sport_col='sports_dict_sport_used', athlete_col='athlete', verbose=False):

## Code

Python example

    # Function to fill missging tags in Sport and Athlete due to partner domain info
    def fill_tags(DF, sport_col='sports_dict_sport_used', athlete_col='athlete', verbose=False):
        
        ' Temporal solution for tags of visits from partnerdomain '
        ' It returns the processed DF '
        ' Ex. my_df = fill_tags(my_df) '
        
        from time import time
        a_=time()
        null_sport_0 = DF[sport_col].isna().sum()
        null_athlete_0 = DF[athlete_col].isna().sum()
        blank_sport_0 = (DF[sport_col].values == "").sum()
        blank_athlete_0 = (DF[athlete_col].values == "").sum()
        
        # Preprocessing
        test_partner = DF.url.apply(lambda x: 'partnerdomain' in x) # Only partnerdomain
        full_partner = DF.loc[test_partner, 'content_title'] # Cases of partnerdomains
        full_selec = DF[DF.content_title.isin(full_partner)] # Cases of partnerdomain + associated website url (with tags)
        test_live = full_selec.url.apply(lambda x: 'live' in x) # No Live
        full_selec = full_selec[~test_live] # No Live
        
        # Create table/dict with tags by content_title (unique)
        test_empty_sport = (DF[sport_col]=='') | (DF[sport_col].isna())
        test_empty_athlete = (DF[athlete_col]=='') | (DF[athlete_col].isna())
        full_selec_tags = full_selec.loc[~(test_empty_sport & test_empty_athlete), [athlete_col,sport_col,'content_title']] 
        full_selec_tags.rename(columns={athlete_col:'athlete_TAG', sport_col:'sport_TAG'}, inplace=True)
        full_selec_tags.drop_duplicates(subset='content_title', keep = 'first', inplace=True)
        
        # Eliminate cases of empty content_title
        test_empty_content_title = (full_selec_tags.content_title=='')
        full_selec_tags = full_selec_tags[~test_empty_content_title]
        
        # Merge retrieved tags and fill the NA and empty strings of partnerdomain with them
        DF = pd.merge(DF, full_selec_tags, left_on='content_title', right_on='content_title', how='left')
        DF[sport_col].fillna(DF['sport_TAG'], inplace=True) # Fill NAs
        DF[athlete_col].fillna(DF['athlete_TAG'], inplace=True) # Fill NAs
        DF.loc[DF[sport_col]=='',sport_col] = DF['sport_TAG'] # Fill ''
        DF.loc[DF[athlete_col]=='',athlete_col] = DF['athlete_TAG'] # Fill ''
        DF.drop(['athlete_TAG','sport_TAG'],axis=1,inplace=True)
        
        null_sport_1 = DF[sport_col].isna().sum()
        null_athlete_1 = DF[athlete_col].isna().sum()
        blank_sport_1 = (DF[sport_col].values == "").sum()
        blank_athlete_1 = (DF[athlete_col].values == "").sum()
        
        b_=time()
        
        if verbose==True:
        
            print(f'Null sports before: {null_sport_0}')
        #     print(f'Blank sports before: {blank_sport_0}\n')
    
            print(f'Null sports after: {null_sport_1}\n')
        #     print(f'Blank sports after: {blank_sport_1}\n')
    
            print(f'Null athletes before: {null_athlete_0}')
        #     print(f'Blank athletes before: {blank_athlete_0}\n')
    
            print(f'Null athletes after: {null_athlete_1}\n')
        #     print(f'Blank athletes after: {blank_athlete_1}\n')
    
            print(f'Percentage of Sport nulls reduced: {round(1-null_sport_1/null_sport_0,4)*100}%')
        #     print(f'Percentage of Sport blanks reduced: {(blank_sport_1-blank_sport_0)}')
            print(f'Percentage of Athlete nulls reduced: {round(1-null_athlete_1/null_athlete_0,4)*100}%\n')
        #     print(f'Percentage of Athlete blanks reduced: {(blank_athlete_1-blank_athlete_0)}\n')
    
            print(f'fill_tags function took {round(b_-a_,2)} seconds')
        
        return DF

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: Pandas
date: 2020-05-07
---
Example Python program Pandas.py


## Code

Python example

    # Pandas read CSV
    df = pd.read_csv('kenmerken.csv', sep=',', dtype={'text': str, 'user_id': str})
    # Write to CSV
    df.to_csv('./dataframe.csv', index = False, header=True)
    # Loop through dataframe
    for i in range(len(df)):
        if df["Naam"][i] == player:
    # Concat two dataframes (put two together)      
    df = pd.concat([df1, df2], axis=1, sort=False)
    # Delete all the rows with NaN in one of the values.
    dfTweets.dropna(inplace = True) 
    df = df[df['text'].notna()]
    # Create empty dataframe with given columns.
    column_names = ["naam", "score", "tweets", "tweetsRac", "proc"]
    dfFinal = pd.DataFrame(columns = column_names)
    # Put all rows in new dataframe if they contain certain string
    df1 = dfTweets[dfTweets["text"].str.contains(achternaam)]
    # Find all the rows with a certain condition
    df2 = df1[df1.ave_profanity > 0]
    # Append row to dataframe
    df8 = {'naam': achternaam, 'score': profanityScore, 'tweets': aantalTweets, 'tweetsRac': aantalTweetsRac, 'proc': procentueel}
    dfFinal = dfFinal.append(df8, ignore_index=True)
    # Drop duplicates in selected column
    df1 = df1.drop_duplicates(subset ="text", keep="first", inplace = False) 
    # Select only specific columns
    df = df[['text','name']]
    
    # Convert data value to ISO standard
    df['date'] = pd.to_datetime(df['date'], dayfirst = False, yearfirst = False)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: nfl_season_standings_w_prob
date: 2020-05-07
---
Example Python program nfl_season_standings_w_prob.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import numpy as np
* import matplotlib.pyplot as plt
* import matplotlib
* # import data
* from collections import defaultdict

## Methods

* def season_prob(apriori):

## Code

Python example

    import numpy as np
    import matplotlib.pyplot as plt
    import matplotlib
    matplotlib.style.use('ggplot')
    %matplotlib inline
    
    # team xref information
    team_xref = pd.read_csv('data/team_xref.csv', sep=';')
    
    print team_xref.shape
    team_xref.head()
    
    # Out
    # (32, 4)
    #           long_name short_name conference   division
    # 0  Arizona Cardinals        ARI        NFC   NFC West
    # 1    Atlanta Falcons        ATL        NFC  NFC South
    # 2   Baltimore Ravens        BAL        AFC  AFC North
    # 3      Buffalo Bills        BUF        AFC   AFC East
    # 4  Carolina Panthers        CAR        NFC  NFC South
    
    
    # import data
    fox_apriori = []
    
    with open('data/FOX_apriori_sup_season.csv', 'r') as f:
        reader = csv.reader(f, delimiter=';')
        next(reader)
        for row in reader:
            fox_apriori.append((row[0], row[1], row[2], row[3], row[4], row[5], float(row[6])))
            
    print len(fox_apriori)
    print "away\thome\taway_conf\thome_conf\taway_div\thome_div\taway_prob"
    fox_apriori[:5]
    
    # Out
    # 256
    # away	home	away_conf	home_conf	away_div	home_div	away_prob
    # [('CAR', 'DEN', 'NFC', 'AFC', 'NFC South', 'AFC West', 0.67),
    # ('BUF', 'BAL', 'AFC', 'AFC', 'AFC East', 'AFC North', 0.553),
    # ('CHI', 'HOU', 'NFC', 'AFC', 'NFC North', 'AFC South', 0.287),
    # ('CIN', 'NYJ', 'AFC', 'AFC', 'AFC North', 'AFC East', 0.479),
    # ('CLE', 'PHI', 'AFC', 'NFC', 'AFC North', 'NFC East', 0.467)]
    
    from collections import defaultdict
    
    def season_prob(apriori):
        
        simple_prob_cnt = defaultdict(lambda : defaultdict(int))
    
        for game in apriori:
            away_team, home_team, away_conf, home_conf, \
                    away_div, home_div, away_prob = game
    
            simple_prob_cnt[away_team]['all'] += away_prob
            simple_prob_cnt[away_team]['away'] += away_prob
            if away_conf == home_conf:
                    simple_prob_cnt[away_team]['conf'] += away_prob
            if away_div == home_div:
                simple_prob_cnt[away_team]['div'] += away_prob
    
            simple_prob_cnt[home_team]['all'] += 1.0 - away_prob
            simple_prob_cnt[home_team]['home'] += 1.0 - away_prob
            if away_conf == home_conf:
                    simple_prob_cnt[home_team]['conf'] += 1.0 - away_prob
            if away_div == home_div:
                simple_prob_cnt[home_team]['div'] += 1.0 - away_prob
                
        return simple_prob_cnt
            
    d = season_prob(fox_apriori)
    
    prob_df = np.around(pd.DataFrame(d), 1).T.fillna(0)
    prob_cols = prob_df.columns
    
    prob_df.columns = ['win_total', 'road_wins', 'conf_wins', 'div_wins', 'home_wins']
    prob_df = prob_df[['win_total', 'home_wins', 'road_wins', 'div_wins', 'conf_wins']]
    
    prob_standings_fox = team_xref.merge(prob_df, left_on='short_name', right_index=True)\
                                    .sort_values(['conference', 'division', 'win_total',
                                              'div_wins', 'conf_wins'], ascending=[1, 1, 0, 0, 0])
        
    print prob_standings_fox.head()
    
    # Out
    #               long_name short_name conference   division  win_total  \
    # 19  New England Patriots         NE        AFC   AFC East        9.5   
    # 22         New York Jets        NYJ        AFC   AFC East        9.4   
    # 3          Buffalo Bills        BUF        AFC   AFC East        7.9   
    # 17        Miami Dolphins        MIA        AFC   AFC East        6.8   
    # 25   Pittsburgh Steelers        PIT        AFC  AFC North       10.7   
    
    #     home_wins  road_wins  div_wins  conf_wins  
    # 19        4.5        5.0       3.5        7.2  
    # 22        4.7        4.7       3.5        6.9  
    # 3         3.9        4.0       2.8        5.8  
    # 17        3.4        3.3       2.2        4.9  
    # 25        5.1        5.6       4.2        7.7  

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

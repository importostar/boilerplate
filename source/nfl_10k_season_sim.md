---
title: nfl_10k_season_sim
date: 2020-05-07
---
Example Python program nfl_10k_season_sim.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import numpy as np
* import matplotlib.pyplot as plt
* import matplotlib
* # import 538 data

## Methods

* def season_sims(game_probabilities, seasons=100):

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
    
    # import 538 data
    fivthir_apriori = []
    
    with open('data/538_apriori_sup_season2.csv', 'r') as f:
        reader = csv.reader(f, delimiter=';')
        next(reader)
        for row in reader:
            fivthir_apriori.append((row[0], row[1], row[2], row[3], row[4], row[5], float(row[6])))
            
    print len(fivthir_apriori)
    print "away\thome\taway_conf\thome_conf\taway_div\thome_div\taway_prob"
    fivthir_apriori[:5]
    
    # Out
    # 256
    # away	home	away_conf	home_conf	away_div	home_div	away_prob
    # [('CAR', 'DEN', 'NFC', 'AFC', 'NFC South', 'AFC West', 0.4),
    #  ('BUF', 'BAL', 'AFC', 'AFC', 'AFC East', 'AFC North', 0.47),
    #  ('CHI', 'HOU', 'NFC', 'AFC', 'NFC North', 'AFC South', 0.33),
    #  ('CIN', 'NYJ', 'AFC', 'AFC', 'AFC North', 'AFC East', 0.49),
    #  ('CLE', 'PHI', 'AFC', 'NFC', 'AFC North', 'NFC East', 0.29)]
    
    # season sim
    np.random.seed(538)
    
    def season_sims(game_probabilities, seasons=100):
        team_win_sim_count = {team: {i:0 for i in range(17)} for team in team_xref.short_name}
    
        away_win_probs = np.array([game[6] for game in game_probabilities])
        samp_season = np.random.random((seasons, len(away_win_probs)))
        # samp_season
    
        samp_away_wins = samp_season < away_win_probs
        samp_home_wins = np.ones((seasons, len(away_win_probs))) - samp_away_wins
    
        for i in range(seasons):
            samp_seasons_cnt = Counter()
            for game,away_w,home_w in zip(game_probabilities, samp_away_wins[i], samp_home_wins[i]):
                away_team, home_team, game_prob = game[0], game[1], game[6]
                samp_seasons_cnt[away_team] += away_w
                samp_seasons_cnt[home_team] += home_w
    
            for team in samp_seasons_cnt:
                team_win_sim_count[team][int(samp_seasons_cnt[team])] += 1
                
        return team_win_sim_count
    
    
    tenK_seasons_538 = pd.DataFrame(season_sims(fivthir_apriori,10000)).T
    tenK_seasons_538

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

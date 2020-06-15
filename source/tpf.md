---
title: tpf
date: 2020-05-07
---
Example Python program tpf.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from prettytable import PrettyTable
* from collections import defaultdict
* import pprint

## Methods

* def __print_table(data):
* def print_tables(data):
* def __match_scores(hg, ag):
* def is_valid_score(row, x): 
* def read_file(file_name):
* def create_tables(args):

## Code

Python example

    #!/usr/bin/python
    
    import sys
    from prettytable import PrettyTable
    from collections import defaultdict
    import pprint
    
    # Columns
    HOME_TEAM = 1
    AWAY_TEAM = 4
    HOME_SCORE = 6
    AWAY_SCORE = 7
    
    POINTS = 0
    GF     = 1
    GA     = 2
    WINS   = 3
    DRAWS  = 4
    LOSSES = 5
    NAME   = 6
    
    sorted_table = lambda tbl: sorted((x for x in tbl.values()), key=lambda y:
            (int(y[POINTS]), int(y[GF])-int(y[GA])), reverse=True)
    row_contents = lambda x: (x[NAME], x[WINS]+x[DRAWS]+x[LOSSES], x[WINS], x[DRAWS],
            x[LOSSES], x[GF], x[GA], x[GF]-x[GA], x[POINTS])
    
    
    def __print_table(data):
        pretty = PrettyTable(['Team', 'Played', 'W', 'D', 'L', 'GF', 'GA', 'GD', 'Pts'])
        print('%s:' % (data[0]))
        for k,v in data[1].iteritems():
            v.append(k)
        map(lambda x: pretty.add_row(row_contents(x)), sorted_table(data[1]))
        print(pretty.get_string())
        print
    
    
    def print_tables(data):
        map(__print_table, data)
    
    
    def __match_scores(hg, ag):
        home = [0, 0, 0, 0, 0, 0]
        away = [0, 0, 0, 0, 0, 0]
        home[GF] = hg
        home[GA] = ag
        away[GF] = ag
        away[GA] = hg
        if hg > ag:
            home[POINTS] = 3
            home[WINS] = 1
            away[LOSSES] = 1
        elif ag > hg:
            away[POINTS] = 3
            away[WINS] = 1
            home[LOSSES] = 1
        else:
            home[POINTS] = 1
            away[POINTS] = 1
            home[DRAWS] = 1
            away[DRAWS] = 1
        return home, away
    
    
    home_goals = lambda row, x: int(row[HOME_SCORE+x*3])
    away_goals = lambda row, x: int(row[AWAY_SCORE+x*3])
    
    
    def is_valid_score(row, x): 
        return not row[HOME_SCORE+x*3].startswith('-') and row[HOME_SCORE+x*3] != ''
    
    
    def read_file(file_name):
        f = open(file_name)
        scores = [[x, {}] for x in f.readline().split(',') if x != '' and x != '\r\n'][:-1]
        lines = (x for x in f.readlines() if not (x.startswith('Subtotal') or x.startswith(',')))
        # Create a dict for each participant
        for row in (x.split(',')[:-1] for x in lines):
            home = row[HOME_TEAM]
            away = row[AWAY_TEAM]
            count = 0
            for participant in scores:
                if is_valid_score(row, count):
                    teams = participant[1]
                    if home not in teams:
                        teams[home] = [0, 0, 0, 0, 0, 0]
                    if away not in teams:
                        teams[away] = [0, 0, 0, 0, 0, 0]
                    points = __match_scores(home_goals(row, count), away_goals(row, count))
                    teams[home] = [x+y for x, y in zip(teams[home], points[0])]
                    teams[away] = [x+y for x, y in zip(teams[away], points[1])]
                count += 1
        return scores
    
    
    def create_tables(args):
    
        if len(args) < 1:
            print('Input file expected')
            exit(1)
        data = read_file(args[0])
        print_tables(data)
    
    
    if __name__ == '__main__':
        create_tables(sys.argv[1:])

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

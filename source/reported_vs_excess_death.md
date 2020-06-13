---
title: reported_vs_excess_death
date: 2020-05-07
---
Example Python program reported_vs_excess_death.py

## Modules

* import pandas as pd
* import matplotlib.pyplot as plt
* import seaborn as sns
* import matplotlib
* import matplotlib.dates as mdates
* from matplotlib.dates import DateFormatter

## Methods

* def get_cumulative_jh_reported(country): 
* def limit_to_our_analysis_window(df, dateCol) :
* def get_economist_weekly_reported_and_excess(country, limitWindow=False) :
* def get_day_of_10th(df, n=10, deathCol="reported_deaths") :
* def timedelta_to_int(s) :
* def add_days_since_10(df, deathCol, dayOf10Deaths) :
* def plot_reported(reported, country) :
* def myFormatter(x, pos):
* def plot_both(reported, excess, country) :
* def myFormatter(x, pos):
* def plot_both_days_since(reported, excess, country) :
* def get_ratio_days_since(country) :
* def plot_country_ratio(countries) :

## Code

Python example

    #!/usr/bin/env python
    # coding: utf-8
    
    # ## Excess COVID-19 mortality vs reported deaths over time
    #  
    # split bar?
    #  
    # y-axis: deaths 
    # x-axis: time
    # 
    # * Pick a country at random, probably from one of those with a good number of deaths. 3-6 countries: US, Brazil, Belgium, Germany, UK
    #  
    # * evidence that the captured proportion of COVID-19 related deaths is non-constant, 
    #  + indication of how much it changes.
    # 
    # * [JHCSSE for reported deaths](https://github.com/CSSEGISandData/COVID-19/tree/master/csse_covid_19_data). 
    # * [The Economist](https://github.com/TheEconomist/covid-19-excess-deaths-tracker) for excess mortality
    
    # In[142]:
    
    
    # Sanity check Economist data
    covid_deaths = 690
    non_covid_deaths = 1659
    expected_deaths = 2059
    total_actual_deaths = covid_deaths + non_covid_deaths
    excess_deaths = total_actual_deaths - expected_deaths
    
    assert(excess_deaths == 290)
    
    
    # In[12]:
    
    
    import pandas as pd
    import matplotlib.pyplot as plt
    import seaborn as sns
    import matplotlib
    import matplotlib.dates as mdates
    from matplotlib.dates import DateFormatter
    
    get_ipython().run_line_magic('matplotlib', 'inline')
    
    sns.set_style('ticks')
    sns.despine()
    
    
    # In[77]:
    
    
    # Keep same order
    jh_countries = [ "US",  "Belgium", "Germany", "United Kingdom" ]
    econ_countries = [ "united_states", "belgium", "germany", "britain", "france", "chile", "switzerland",                  "italy", "netherlands", "spain", "sweden"]
    nyt_countries = [ "US",  "Belgium", "Germany", "United Kingdom", "France" ]
    
    
    # In[28]:
    
    
    JH_PATH = r"COVID-19/csse_covid_19_data/"
    CUMUL_CONF_DEATHS_PATH = JH_PATH + r"csse_covid_19_time_series/time_series_covid19_deaths_global.csv"
    
    ECON_PATH = r"covid-19-excess-deaths-tracker/output-data/excess-deaths/"
    
    
    # In[78]:
    
    
    def get_cumulative_jh_reported(country): 
        confirmed = pd.read_csv(CUMUL_CONF_DEATHS_PATH)
        country_confirmed = confirmed[(confirmed['Country/Region'] == country)                                    & confirmed['Province/State'].isnull() ]
        country_confirmed = country_confirmed.drop(["Province/State", "Country/Region", "Lat", "Long"], axis=1)
        tuples = pd.melt(country_confirmed, var_name='date')
        tuples["date"] = pd.to_datetime(tuples["date"], format='%m/%d/%y')
        tuples.columns = ["date", "reported_deaths"]
        
        return tuples
    
    
    def limit_to_our_analysis_window(df, dateCol) :
        windowStart = pd.to_datetime("2020-01-22", format='%Y-%m-%d')
        windowEnd = pd.to_datetime("2020-04-25", format='%Y-%m-%d')
        df["timestamps"] = pd.to_datetime(df[dateCol], format='%Y-%m-%d')
        
        return df[ (df["timestamps"] >= windowStart)               & (df["timestamps"] <= windowEnd)]
    
    
    def get_economist_weekly_reported_and_excess(country, limitWindow=False) :
        excess_country_path = ECON_PATH + country + "_excess_deaths.csv"
        econ_country = pd.read_csv(excess_country_path)
        ECON_DATE_COL = "start_date"
        
        if limitWindow :
            econ_country = limit_to_our_analysis_window(econ_country, ECON_DATE_COL)
        
        # If there's a national summary, just use that
        if country in ["britain", "france", "chile", "italy", "spain"] :
            econ_country = econ_country[econ_country.region == country.capitalize()]
    
        reported_sum = econ_country[[ECON_DATE_COL, "covid_deaths"]].groupby(ECON_DATE_COL)                         .sum().reset_index()
        excess_sum = econ_country[[ECON_DATE_COL, "excess_deaths"]].groupby(ECON_DATE_COL)                     .sum().reset_index()
    
        reported_sum.columns = ["date", "reported_deaths"]
        excess_sum.columns = ["date", "excess_deaths"]
        reported_sum["date"] = pd.to_datetime(reported_sum["date"], format='%Y-%m-%d')
        excess_sum["date"] = pd.to_datetime(excess_sum["date"], format='%Y-%m-%d')
        
        return reported_sum, excess_sum
    
    
    def get_day_of_10th(df, n=10, deathCol="reported_deaths") :
        return df[df[deathCol] >= n]["date"]                     .sort_values()                     .iloc[0]
    
    
    def timedelta_to_int(s) :
        return s.astype('str').str.replace(" days 00:00:00.000000000", "")             .astype("int8")
    
    
    def add_days_since_10(df, deathCol, dayOf10Deaths) :
        df = df[df["date"] >= dayOf10Deaths]
        df["daysSince10th"] = (df["date"] - dayOf10Deaths) 
        df["daysSince10th"] = timedelta_to_int(df["daysSince10th"])
        
        return df
    
    
    def plot_reported(reported, country) :
        fig, ax = plt.subplots()
        sns.tsplot(data = reported['reported_deaths'], time = reported['date'],                ax=ax)
    
        def myFormatter(x, pos):
            return pd.to_datetime(x).strftime('%b-%d')
    
        ax.get_yaxis().set_major_formatter(
            matplotlib.ticker.FuncFormatter(lambda x, p: format(int(x), ','))
        )
    
        ax.xaxis.set_major_formatter(
            matplotlib.ticker.FuncFormatter(myFormatter)
        )
        plt.show()
    
    
    def plot_both(reported, excess, country) :
        fig, ax = plt.subplots()
        sns.tsplot(data = reported['reported_deaths'], time = reported['date'],                ax=ax)
    
        def myFormatter(x, pos):
            return pd.to_datetime(x).strftime('%b-%d')
    
        ax.get_yaxis().set_major_formatter(
            matplotlib.ticker.FuncFormatter(lambda x, p: format(int(x), ','))
        )
    
        ax.xaxis.set_major_formatter(
            matplotlib.ticker.FuncFormatter(myFormatter)
        )
        
        sns.tsplot(data = excess['excess_deaths'], time = excess['date'],                ax=ax, color="green")
        
        ax.set_ylabel("Weekly deaths")
        ax.set_xlabel("Date")
        plt.subplots_adjust(left=.2)
        tit = country.replace("_", " ").title()
        plt.title(tit, fontsize=20)
        h = plt.gca().get_lines()
        plt.legend(handles=h, labels=["reported COVID", "excess"])
    
        plt.savefig('{}.png'.format(country), dpi=300)
        plt.savefig('{}.pdf'.format(country), dpi=300)
    
        plt.show()
        
        
    def plot_both_days_since(reported, excess, country) :
        fig, ax = plt.subplots()
        sns.lineplot(y = reported['reported_deaths'], x = reported['daysSince10th'],                    ax=ax)
        sns.lineplot(y = excess['excess_deaths'], x = excess['daysSince10th'],                    ax=ax)
        
        ax.set_ylabel("Weekly deaths")
        ax.set_xlabel("Days since 10th reported COVID death")
        plt.subplots_adjust(left=.2)
        tit = country.replace("_", " ").title()
        plt.title(tit, fontsize=20)
        h = plt.gca().get_lines()
        plt.legend(handles=h, labels=["reported COVID", "excess"])
    
        plt.savefig('{}.png'.format(country), dpi=300)
        plt.savefig('{}.pdf'.format(country), dpi=300)
    
        plt.show()
        
        
    
    
    # # JH cumulative deaths
    
    # In[30]:
    
    
    for country in jh_countries :
        tuples = get_cumulative_jh_reported(country)
        plot_reported(tuples, country)
    
    
    # # Economist data with dates
    
    # In[79]:
    
    
    for country in econ_countries :
        reported, excess = get_economist_weekly_reported_and_excess(country, limitWindow=True)
        plot_both(reported, excess, country)
    
    
    # # Redo Econist with days since 10th covid death
    
    # In[85]:
    
    
    for country in econ_countries :
        reported, excess = get_economist_weekly_reported_and_excess(country)
        dayOf10Deaths = get_day_of_10th(reported)
        reported = add_days_since_10(reported, "reported_deaths", dayOf10Deaths)
        excess = add_days_since_10(excess, "excess_deaths", dayOf10Deaths)
        
        plot_both_days_since(reported, excess, country)
        
    
    
    # # International ratios 
    # 
    # $c / e$
    
    # In[140]:
    
    
    econ_countries_ratio = [ "united_states", "britain", "chile",                           "sweden", "netherlands", "spain",                         "belgium", "switzerland", "france"] # "italy",
    
    def get_ratio_days_since(country) :
        reported, excess = get_economist_weekly_reported_and_excess(country)
        dayOf10Deaths = get_day_of_10th(reported)
        reported = add_days_since_10(reported, "reported_deaths", dayOf10Deaths)
        excess = add_days_since_10(excess, "excess_deaths", dayOf10Deaths)
        both = excess.merge(reported, on="date")             [["daysSince10th_x", "excess_deaths","reported_deaths"]]
        both.columns = ["daysSince10th", "excess_deaths","reported_deaths"]
        both["ratio"] = both["reported_deaths"] / both["excess_deaths"]
        
        return both
        
    
    
    def plot_country_ratio(countries) :
        fig, ax = plt.subplots()
    
        for country in countries :
            both = get_ratio_days_since(country)
            sns.lineplot(y = both['ratio'], x = both['daysSince10th'],                        ax=ax, label=country)
    
        ax.set_ylabel("Ratio of reported to excess")
        ax.set_xlabel("Days since 10th reported COVID death")
        plt.subplots_adjust(left=.15)
        plt.legend()
        #tit = country.replace("_", " ").title()
        #plt.title(tit, fontsize=20)
        #h = plt.gca().get_lines()
        #plt.legend(handles=h, labels=["reported / excess"])
    
        #plt.ylim(ymin=0)
    
        plt.savefig('{}_ratio.png'.format("_".join(countries)), dpi=300)
        #plt.savefig('{}.pdf'.format("c_e_ratio"), dpi=300)
    
        plt.show()
    
    
    plot_country_ratio(econ_countries_ratio[:3])
    plot_country_ratio(econ_countries_ratio[3:6])
    plot_country_ratio(econ_countries_ratio[6:])
    
    
    # In[122]:
    
    
    get_ratio_days_since("britain")
    
    
    # # Compare Economist excess to NYT
    # 
    # [NYT doesn't actually have the reported COVID death counts](https://github.com/nytimes/covid-19-data/blob/master/excess-deaths/deaths.csv)
    # 
    
    # In[ ]:
    
    
    NYT_PATH = "nytimes/excess-deaths/deaths.csv"
    
    df = pd.read_csv(NYT_PATH)
    
    weekly_nationals = df[(df.frequency == "weekly") & df.placename.isnull()]
    
    
    # In[ ]:
    
    
    
    
    
    # In[ ]:
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

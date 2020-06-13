---
title: top10_deadliest_houses_got
date: 2020-05-07
---
Example Python program top10_deadliest_houses_got.py


## Code

Python example

    #Creating the plot & setting up the data we´re plotting, in this case, the value count of deaths ocurred per Killers House, as each log represents one death. 
    fig, ax = plt.subplots()
    data = dataset["Killers House"].value_counts().head(10)
    
    #Setting the x & y axis to the index and values of our "data" series 
    x_data = data.index
    y_data = data.values
    
    #Plotting the data itself 
    ax.bar(x_data , y_data)
    
    #Adding shorter labels to the top 10 visualized for improved readability 
    Labels = ["Targaryen", "Lannister", "Stark", "White Walkers", "Bolton", "Night´s Watch", "Free Folk", "Greayjoy", "Sons of the Harpy", "Baratheon"]
    
    #Customizing other aspects of the graph such as Title, labels, and the ° rotation of the x axis labels. 
    ax.set_title("Deaths by House") 
    ax.set_xlabel("House") 
    ax.set_ylabel("Deaths")
    plt.xticks(x_data, labels = Labels, rotation=90)
    plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

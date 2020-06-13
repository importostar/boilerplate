---
title: word_counter
date: 2020-05-07
---
Example Python program word_counter.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import subprocess
* import argparse
* import csv
* from datetime import datetime, timedelta
* from pathlib import Path
* import numpy as np
* import matplotlib
* import matplotlib.pyplot as plt
* # import pdb; pdb.set_trace()

## Code

Python example

    import subprocess
    import argparse
    import csv
    from datetime import datetime, timedelta
    from pathlib import Path
    
    import numpy as np
    import matplotlib
    import matplotlib.pyplot as plt
    
    # Create the parser
    parser = argparse.ArgumentParser()
    # Create arguments
    parser.add_argument(
        "-p", "--plot",
        help="Plot thesis progress",
        action="store_true"
    )
    parser.add_argument(
        "-n", "--no_append",
        help="Disable adding word count it to the csv",
        action="store_true"
    )
    parser.add_argument(
        "-w", "--words",
        help="The target number of words for the thesis",
        type=int,
        default=40000
    )
    parser.add_argument(
        "-e", "--end",
        help="The target date for thesis compeltion",
        type=str,
        default="2019-11-02"
    )
    parser.add_argument(
        "-st", "--start",
        help="The start date for thesis writing",
        type=str,
        default="2019-07-26"
    )
    parser.add_argument(
        "-s", "--save",
        help="Save the plot",
        action="store_true"
    )
    parser.add_argument(
        "-c", "--current_progress",
        help="Print current and target number of words",
        action="store_true"
    )
    parser.add_argument(
        "-exp", "--exponent",
        help="Exponent for expected progress",
        type=float,
        default=1.1
    )
    parser.add_argument(
        "-o", "--order",
        help="Order for the polynomial fit for current progress",
        type=int,
        default=1
    )
    # Parse arguments
    args = parser.parse_args()
    
    # Append the word count unless told not to
    if not args.no_append or args.current_progress:
        # Texcount command to calculate the number of words in the thesis
        # Hardcoded filename
        cmd = "texcount -1 -sum -relaxed -inc thesis_main.tex"
        # Use subprocess to capture the output
        wordcount = int(subprocess.run(cmd.split(" "), stdout=subprocess.PIPE).stdout.decode('utf-8'))
        # Overwrite the word.count file for the muthesis.cls
        cmd = f"/bin/echo {wordcount} > word.count"
        subprocess.run(cmd, shell=True)
        # Create the row to be added to the
        new_row = [datetime.now().strftime("%Y-%m-%d_%H:%M:%S"), wordcount]
        # Only add to csv if not told not to
        if not args.no_append:
            # Ensure that the csv exists (if this is the first time running)
            csv_path = Path(Path.cwd() / "word_counts.csv").touch(exist_ok=True)
            # Write the new row to the file (use append mode)
            with open("word_counts.csv", "a") as csv_file:
                writer = csv.writer(csv_file)
                writer.writerow(new_row)
    
    if args.current_progress or args.plot:
        # Read in the data
        with open("word_counts.csv") as csv_file:
            reader = csv.reader(csv_file)
            data = [row for row in reader]
        # Extract the info from the csv and format
        dates = [datetime.strptime(d, "%Y-%m-%d_%H:%M:%S") for d, _ in data]
        numeric_dates = [matplotlib.dates.date2num(d) for d in dates]
        words = [int(words) for _, words in data]
        # Get the start and end dates from command line
        start_date = datetime.strptime(args.start, "%Y-%m-%d")
        end_date = datetime.strptime(args.end, "%Y-%m-%d")
        start_date_mpl = matplotlib.dates.date2num(start_date)
        end_date_mpl = matplotlib.dates.date2num(end_date)
        # Calculate expected progress (set to 1 for linear)
        expon = args.exponent
        coeff = args.words/(((end_date-start_date).days)**(expon))
    
    if args.current_progress:
        # Calculate expected words per day
        words_per_day = args.words/((end_date-start_date).days)
        # Calculate what we should be on
        target_words = coeff*((datetime.now() - start_date).days)**expon
        text = f"For {datetime.now().strftime('%Y-%m-%d')}:\n" \
                f"Current #words: {wordcount}\n" \
                f"Target #words: {int(target_words)}\n" \
                f"Difference: {int(wordcount - target_words)} words"
        print(text)
    
    # Plot the results
    if args.plot:
        # Create figure & axis
        fig, ax = plt.subplots(figsize=(12,8))
        # Plot current progress
        ax.plot_date(
            numeric_dates,
            words,
            marker="D",
            markersize=4,
            color="black",
            linestyle="solid",
            linewidth=1.75,
            label="Actual progress"
        )
        # Get a range across the times
        date_range = [start_date + timedelta(days=x) for x in range(0, (end_date-start_date).days+1)]
        date_range = [matplotlib.dates.date2num(d) for d in date_range]
        # Get the coefficients for line of best fit
        if args.order == 1:
            m, c = np.polyfit(numeric_dates, words, 1)#, w=np.arange(len(words))**2)
            preds = [num_date*m + c for num_date in date_range]
        elif args.order == 2:
            m2, m, c = np.polyfit(numeric_dates, words, 2, w=np.arange(len(words)))
            preds = [(num_date**2)*m2 + num_date*m + c for num_date in date_range]
        # import pdb; pdb.set_trace()
        # Plot extrapolated line based on current progress
        ax.plot_date(
            date_range,
            preds,
            marker=None,
            linestyle="dotted",
            linewidth=1.1,
            color="royalblue",
            label="Extrapolated progress"
        )
        # Plot a linear line for the number of words expected to write
        ax.plot_date(
            # [start_date, end_date],
            # [0, int(args.words)],
            date_range,
            [coeff*(date-start_date_mpl)**expon for date in date_range],
            marker=None,
            linestyle="dashed",
            color="green",
            linewidth=1.1,
            label="Expected progress"
        )
        # Get current y-lims
        ylims = plt.ylim()
        # Show today's date
        ax.plot_date(
            [matplotlib.dates.date2num(datetime.now())]*2,
            [0, ylims[1]], # Get the upper y-limit
            marker=None,
            linestyle="dotted",
            linewidth=0.75,
            color="darkred",
            label="Today"
        )
        # Set the label
        ax.set_xlabel("Date (every Friday)")
        # Set the date ticks to every Friday
        ax.xaxis.set_major_locator(
            matplotlib.dates.WeekdayLocator(
                byweekday=5,
                interval=1
            )
        )
        # Format it to shown the month and day
        ax.xaxis.set_major_formatter(
            matplotlib.dates.DateFormatter('%m-%d')
        )
        ax.set_ylabel("Number of Words")
        ax.legend()
        # Reset ylim
        plt.gca().set_ylim(bottom=0, top=ylims[1])
        # Save or show the plot
        if args.save:
            plt.savefig(
                "thesis_progress.png",
                format="png",
                dpi=200,
                bbox_inches="tight"
            )
        else:
            plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

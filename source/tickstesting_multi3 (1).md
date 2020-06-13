---
title: tickstesting_multi3 (1)
date: 2020-05-07
---
Example Python program tickstesting_multi3 (1).py


## Code

Python example

    nrow=3
    ncol=4
    fig = plt.figure(figsize=[10,6])
    for ipan in range(nrow*ncol):
        therow = int( (ipan-(ipan % ncol))/ncol ) +1  # 1 to nrow
        thecol = (ipan % ncol) +1                     # 1 to ncol
        #pan = ipan + 1          (not needed)         # 1 to nrow*nrol
        ax = fig.add_subplot(nrow,ncol,ipan+1)
        ax.plot(x,y, linestyle="none",marker="o",alpha=0.5)
        ax.axvline(0,linestyle=":",color="grey")
        ax.axhline(0,linestyle=":",color="grey")
        ax.plot( (-20,20),(-20,20),linestyle=":",color="grey")
        ax.text(0.05,0.85, ipan, transform=ax.transAxes)
        ax.set_xlabel('Input'  if ipan>=(nrow*(ncol-1)-1) else "" )
        ax.set_ylabel('Output' if (ipan%ncol)==0          else "" ) 
        ax.set_xlim( -4, 14 )
        ax.set_ylim(-10, 15 )
        ax.xaxis.set_major_locator(matplotlib.ticker.MultipleLocator(5.0))
        ax.xaxis.set_minor_locator(matplotlib.ticker.MultipleLocator(1.0))
        ax.yaxis.set_major_locator(matplotlib.ticker.MultipleLocator(5.0))
        ax.yaxis.set_minor_locator(matplotlib.ticker.MultipleLocator(1.0))
        if therow==1 or therow==nrow:
            # only number on top and bottom row
            if therow==1:
                ax.tick_params(axis="x",which="both",
                               labelbottom=False, labeltop=True)
            if therow==nrow:
                ax.tick_params(axis="x",which="both",
                               labelbottom=True, labeltop=False)
            ax.xaxis.set_major_formatter(matplotlib.ticker.ScalarFormatter())
        else:
            ax.tick_params(axis="x",which="both",
                           labelbottom=False, labeltop=False)
            ax.xaxis.set_major_formatter(matplotlib.ticker.NullFormatter())
        ax.tick_params(axis="x",which="both",direction="in", bottom=True, top=True)
        #
        if thecol==1 or thecol==ncol:
            # only number on 1st and last column
            if thecol==1:
                ax.tick_params(axis="y",which="both",
                               labelleft=True, labelright=False)
            if thecol==ncol:
                ax.tick_params(axis="y",which="both",
                               labelleft=False, labelright=True)
                ax.yaxis.set_major_formatter(matplotlib.ticker.ScalarFormatter())
        else:
            ax.tick_params(axis="y",which="both",
                           labelleft=False, labelright=False)
            ax.yaxis.set_major_formatter(matplotlib.ticker.NullFormatter())
        ax.tick_params(axis="y",which="both",direction="in",left=True, right=True)
    
    fig.subplots_adjust(top=0.95, bottom=0.09, left=0.07, right=0.95,
                        hspace=0.08, wspace=0.05)
    plt.show()
    plt.close()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

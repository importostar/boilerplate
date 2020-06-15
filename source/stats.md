---
title: stats
date: 2020-05-07
---
Example Python program stats.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import datetime
* import matplotlib
* import codecs
* import matplotlib.dates
* import matplotlib.pyplot

## Methods

* def plotify(artistname, songname, albumname, filename):

## Code

Python example

    # -*- coding: utf-8 -*-
    
    import datetime
    import matplotlib
    import codecs
    
    # history downloaded with lastexport.py https://gist.github.com/bitmorse/5201491
    fp = codecs.open("tracks.txt", "r", "utf8")
    
    albums = {}
    artists = {}
    songs = {}
    plotdata = {}
    
    data = []
    
    date1 = None
    date2 = None
    
    for line in fp.readlines():
        line = line.split("\t")
        time = line[0]
        song = line[1]
        artist = line[2]
        album = line[3]
        if artist.startswith(u"若"): artist = "Hajime Wakai"
        if artist.startswith(u"中"): artist = "Megumi Nakajima"
        if artist.startswith(u"近"): artist = "Koji Kondo"
        if artist.startswith(u"山"): artist = "Michiru Yamane"
        if artist.startswith(u"任"): artist = "Nintendo"
        if artist.startswith(u"広"): artist = "Kohmi Hirose"
        time = datetime.datetime.utcfromtimestamp(int(time))
        time = datetime.datetime(time.year, time.month, 1)
        if date1 is None:
            date1 = time
            date2 = time
        else:
            date1 = min(date1, time)
            date2 = max(date2, time)
        data.append((time, song, artist, album))
    
    # hack
    date2 = datetime.datetime(date2.year, date2.month + 1, 1)
    
    for (time, song, artist, album) in data:
        artists[artist] = artists.get(artist, 0) + 1
        songs[(artist, song)] = songs.get((artist, song), 0) + 1
        albums[(artist, album)] = albums.get((artist, album), 0) + 1
    
    def plotify(artistname, songname, albumname, filename):
        import matplotlib.dates
        import matplotlib.pyplot
        matplotlib.pyplot.clf()
        plotdata = {}
        for (time, song, artist, album) in data:
            if (songname is None or songname == song) and \
                (artistname is None or artistname == artist) and \
                (albumname is None or albumname == album):
                plotdata[time] = plotdata.get(time, 0) + 1
        plotx = []
        ploty = []
        for dt, cnt in sorted(plotdata.items()):
            plotx.append(dt)
            ploty.append(cnt)
        fig = matplotlib.pyplot.gcf()
        fig.set_size_inches(25, 5)
        matplotlib.pyplot.bar(plotx, ploty, width=20)
        matplotlib.pyplot.xlim([date1, date2])
        if songname is None:
            if albumname is None:
                if artistname is None:
                    matplotlib.pyplot.title("All songs")
                else:
                    matplotlib.pyplot.title(u"%s (all songs)" % artistname)
            else:
                matplotlib.pyplot.title(u"%s - %s (album)" % (artistname, albumname))
        else:
                matplotlib.pyplot.title(u"%s - %s (song)" % (artistname, songname))
        matplotlib.pyplot.savefig(filename, bbox_inches="tight", dpi=70)
        matplotlib.pyplot.savefig(filename.replace(".png", "_thumb.png"), bbox_inches="tight", dpi=8)
    
    albums = [(c, v) for (v, c) in albums.items()]
    artists = [(c, v) for (v, c) in artists.items()]
    songs = [(c, v) for (v, c) in songs.items()]
    
    albums.sort(reverse=True)
    artists.sort(reverse=True)
    songs.sort(reverse=True)
    
    
    op = codecs.open("scrobbles.html", "w", "utf8")
    
    op.write("""<html><head>
    <meta charset="UTF-8">
    <style>body, table { font-family: sans-serif; font-size: 14px; }
    table { border-collapse: collapse; } table, th, td { border: 1px solid black; padding: 2px; }
    td { max-width: 300px; }</style></head><body>""")
    
    op.write("<h2>Totals</h2>")
    
    op.write("<p>Scrobbles: %i</p>" % len(data))
    op.write("<p>Artists: %i</p>" % len(artists))
    op.write("<p>Albums: %i</p>" % len(albums))
    op.write("<p>Songs: %i</p>" % len(songs))
    
    plotify(None, None, None, "total.png")
    op.write("""<img src="total.png"/>""")
    
    op.write("<h2>Artists</h2>")
    op.write("<table>")
    for i in range(len(artists)):
        if artists[i][0] >= 10:
            print "artist", i
            op.write(u"<tr><td>%i</td> <td>%s</td> <td>%i</td> " % \
                (i+1, artists[i][1], artists[i][0]))
            if i < 50:
                plotify(artists[i][1], None, None, "artists_%i.png" % i)
                op.write("""<td><a href="artists_%s.png"><img src="artists_%s_thumb.png"/></a></td></tr>\n""" % (i, i))
            else:
                op.write("""<td></td></tr>\n""")
    op.write("</table>")
    
    op.write("<h2>Albums</h2>")
    op.write("<table>")
    for i in range(len(albums)):
        if albums[i][0] >= 10:
            print "album", i
            op.write(u"<tr><td>%i</td> <td>%s</td> <td>%s</td> <td>%i</td>\n" % \
                (i+1, albums[i][1][0], albums[i][1][1], albums[i][0]))
            if i < 50:
                plotify(albums[i][1][0], None, albums[i][1][1], "albums_%i.png" % i)
                op.write("""<td><a href="albums_%s.png"><img src="albums_%s_thumb.png"/></a></td></tr>\n""" % (i, i))
            else:
                op.write("""<td></td></tr>\n""")
    op.write("</table>")
    
    op.write("<h2>Songs</h2>")
    op.write("<table>")
    for i in range(len(songs)):
        if songs[i][0] >= 10:
            print "song", i
            op.write(u"<tr><td>%i</td> <td>%s</td> <td>%s</td> <td>%i</td>\n" % \
                (i+1, songs[i][1][0], songs[i][1][1], songs[i][0]))
            if i < 50:
                plotify(songs[i][1][0], songs[i][1][1], None, "songs_%i.png" % i)
                op.write("""<td><a href="songs_%s.png"><img src="songs_%s_thumb.png"/></a></td></tr>\n""" % (i, i))
            else:
                op.write("""<td></td></tr>\n""")
    op.write("</table>")
    op.write("</body></html>")
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

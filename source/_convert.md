---
title: _convert
date: 2020-05-07
---
Example Python program _convert.py


## Methods

* def _convert(chart):

## Code

Python example

    _line_mapping = {
        'x': lambda d: ('x', d),
        'y': lambda d: ('y', d),
        'args': lambda x, y: [x, y]
    }
    
    def _convert(chart):
        """Convert an altair encoding to a Matplotlib figure
        Parameters
        ----------
        chart
            The Altair chart.
        Returns
        -------
        mapping : dict
            Mapping from parts of the encoding to the Matplotlib artists.  This is
            for later customization.
        """
        mapping = {}
    
        if not chart.to_dict().get('encoding'):
            raise ValueError("Encoding not provided with the chart specification")
    
        for enc_channel, enc_spec in chart.to_dict()['encoding'].items():
            if not _allowed_ranged_marks(enc_channel, chart.to_dict()['mark']):
                raise ValueError("Ranged encoding channels like x2, y2 not allowed for Mark: {}".format(chart['mark']))
    
        for channel in chart.to_dict()['encoding']:
            data = _locate_channel_data(chart, channel)
            dtype = _locate_channel_dtype(chart, channel)
            # FROM AXIS-NUMERIC============================================================================================
            if dtype == 'temporal':
                data = _convert_to_mpl_date(data)
            # END STUFF FROM AXIS-NUMERIC==================================================================================
            """
            if dtype == 'temporal':
                try:
                    data = mdates.date2num(data)  # Convert dates to Matplotlib dates
                except AttributeError:
                    raise
            """
    
            if chart.mark in ['point', 'circle', 'square']:
                mapping[_mappings[channel](dtype, data)[0]] = _mappings[channel](dtype, data)[1]
            elif chart.mark == 'line' and channel in ['x', 'y']:
                mapping[_line_mapping[channel](data)[0]] = _line_mapping[channel](data)[1]
    
        if chart.mark == 'line':
            mapping['args'] = _line_mapping['args'](mapping['x'], mapping['y'])  # plot() doesn't take kwargs for x and y
        
        return mapping

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

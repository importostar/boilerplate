---
title: converter_template
date: 2020-05-07
---
Example Python program converter_template.py

## Modules

* import csv
* import sys
* from functools import partial

## Methods

* def create_reader():
* def create_writer():
* def run_pipeline(steps, rows):
* def convert(rows):
* def fit_to_output_format(rows):
* def process(reader, writer):
* def main():

## Code

Python example

    """ Convert each record """
    import csv
    import sys
    from functools import partial
    
    
    INPUT_FIELDS = (
        'col1',
        'col2',
        'col3',
    )
    
    OUTPUT_FIELDS = (
        'col4',
        'col5',
    )
    
    
    def create_reader():
        """ Create DictReader. """
        return csv.DictReader(sys.stdin, fieldnames=INPUT_FIELDS)
    
    
    def create_writer():
        """ Create DictWriter. """
        return csv.DictWriter(sys.stdout, fieldnames=OUTPUT_FIELDS)
    
    
    def run_pipeline(steps, rows):
        """ process steps. """
        tmp = rows
        for step in steps:
            tmp = step(tmp)
    
    
    def convert(rows):
        """
        DO SOMETHING.
        """
        return rows
    
    
    def fit_to_output_format(rows):
        """ Fit to the output format. """
    
        for row in rows:
            yield {
                'row4': row['row1'],
                'row5': row['row2'],
    
            }
    
    
    def process(reader, writer):
        """ Main process """
    
        steps = (
            convert,
            fit_to_output_format,
            partial(filter, lambda x: x['row1'] != ''),
            writer.writerows,
            )
        run_pipeline(steps, reader)
    
    
    def main():
        """ Main """
    
        reader = create_reader()
        writer = create_writer()
    
        process(reader, writer)
    
    
    if __name__ == '__main__':
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

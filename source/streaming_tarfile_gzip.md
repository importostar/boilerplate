---
title: streaming_tarfile_gzip
date: 2020-05-07
---
Example Python program streaming_tarfile_gzip.py

## Modules

* import gzip
* import tarfile

## Code

Python example

    import gzip
    import tarfile
    
    with open('files.tar.gz') as f:
    
        # this should preserve the file object stream from http response to gzip stream to tarfile
        archive = tarfile.open(fileobj=gzip.GzipFile(fileobj=f), mode='r|')
    
        # since archive is a stream, you cannot perform random access
        # but instead you can pattern match against each entry
        while True:
            file = archive.next()
            if file is None:
                break
            if file.name == 'X':
                file_x = archive.extractfile(file)
                # you need to read it HERE
                # else the cursor will stream on and you can't seek backwards
                file_x.read()
            elif file.name == 'Y':
                file_y = archive.extractfile(file)
                # you need to read it HERE
                # else the cursor will stream on and you can't seek backwards
                file_y.read()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

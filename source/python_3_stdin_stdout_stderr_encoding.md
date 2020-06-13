---
title: python_3_stdin_stdout_stderr_encoding
date: 2020-05-07
---
Example Python program python_3_stdin_stdout_stderr_encoding.py

## Modules

* import sys
* import io

## Code

Python example

    import sys
    import io
    
    # Python 3's std stream encoding is determined by locale or `PYTHONIOENCODING` environment variables
    # however if you want to explicitly maintain an encoding regardless of environment
    # you need to do this:
    
    sys.stdin = io.TextIOWrapper(
        sys.stdin.buffer,
        encoding='utf-8',
        errors=sys.stdin.errors,
        newline=sys.stdin.newlines,
        line_buffering=sys.stdin.line_buffering)
    
    sys.stdout = io.TextIOWrapper(
        sys.stdout.buffer,
        encoding='utf-8',
        errors=sys.stdout.errors,
        newline=sys.stdout.newlines,
        line_buffering=sys.stdout.line_buffering)
    
    sys.stderr = io.TextIOWrapper(
        sys.stderr.buffer,
        encoding='utf-8',
        errors=sys.stderr.errors,
        newline=sys.stderr.newlines,
        line_buffering=sys.stderr.line_buffering)
    
    # the last parameter `write_through` does not appear to be perserved in the existing streams
    # it would be prudent to find out the value of `write_through` for the original streams
    # and pass them along if you **only** want to change the encoding of the streams
    
    # furthermore for any `open` calls, you must pass the `encoding` parameter

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

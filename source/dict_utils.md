---
title: dict_utils
date: 2020-05-07
---
Example Python program dict_utils.py


## Methods

* def prefix_dict(prefix, d):
* def unprefix_dict(prefix, d):
* def suffix_dict(suffix, d):
* def unsuffix_dict(suffix, d):
* def rekey_dict(keys, d):
* def transform_dict(filters, d, out=None):

## Code

Python example

    def prefix_dict(prefix, d):
        return {(prefix + k): v for (k, v) in d.items()}
    
    
    def unprefix_dict(prefix, d):
        return {(k[len(prefix):] if k.startswith(prefix) else k): v
                for (k, v) in d.items()}
    
    
    def suffix_dict(suffix, d):
        return {(k + suffix): v for (k, v) in d.items()}
    
    
    def unsuffix_dict(suffix, d):
        suffix_len = len(suffix)
        return {(k[:len(k) - suffix_len] if k.endswith(suffix) else k): v
                for (k, v) in d.items()}
    
    
    # rekeys a dictionary with a key map
    # beware if rekeying into an existing key
    # the later key in the dictionary will override
    def rekey_dict(keys, d):
        return {keys.get(k, k): v for (k, v) in d.items()}
    
     
    # transform a dictionary based on a dictionary of transforms
    # the transforms should be lamdas
    def transform_dict(filters, d, out=None):
        out_ = {} if out is None else out
        for (k, v) in d.items():
            f = filters.get(k)
            if f is not None:
                out_[k] = f(v)
            else:
                out_[k] = v
        return out_

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

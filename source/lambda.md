---
title: lambda
date: 2020-05-07
---
Example Python program lambda.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import http
* import json
* import importlib
* import os
* import pkgutil
* import re
* import sys
* import boto3
* imp = importlib.import_module(pkg)

## Methods

* def handler(_event: dict, _context: dict) -> dict:
* def get_pkg_version(pkg: str) -> str:
* def prune_versions(versions: list) -> list:
* def make_status(code, msg='') -> dict:

## Code

Python example

    #!/usr/bin/env python3.7
    '''
    List all of the installed packages in the environment and write them
    to the S3 bucket.
    '''
    import http
    import json
    import importlib
    import os
    import pkgutil
    import re
    import sys
    
    import boto3
    
    try:
        S3_BUCKET = os.environ['S3_BUCKET']
    except KeyError:
        S3_BUCKET = None
    PYVER = f'python-{sys.version_info[0]}.{sys.version_info[1]}.{sys.version_info[2]}'
    VERSION_PATTERN = re.compile(r'^.*version.*$', re.IGNORECASE)
    
    
    def handler(_event: dict, _context: dict) -> dict:
        '''
        Generate the list of installed packages.
        '''
        pkgs = []
        ##names = [f'{m.name}' for m in pkgutil.iter_modules() if m.ispkg]
        names = [f'{m.name}' for m in pkgutil.iter_modules()]
        names += list(sys.builtin_module_names)
        num_native = 0
        num_installed = 0
        for pkg in names:
            version = get_pkg_version(pkg)
            pkgs.append(f'{pkg}=={version}')
            if 'python' in version:
                num_native += 1
            else:
                num_installed += 1
        body = {'total': len(pkgs),
                'num_native': num_native,
                'num_installed': num_installed,
                'pkgs': sorted(pkgs, key=lambda s: s.lstrip('_').lower())}
        content = '\n'.join([f'# python: {i}' for i in sys.version.split('\n')])
        content += '\n'
        content += f'# num_native:    {num_native:>4}\n'
        content += f'# num_installed: {num_installed:>4}\n'
        content += f'# total:         {len(pkgs):>4}\n'
        content += '\n'.join(sorted(pkgs, key=lambda s: s.lstrip('_').lower())) + '\n'
        if not S3_BUCKET:
            ofp = sys.stdout
            ofp.write(content)
        else:
            # To view the data, highlighting the non-native packages.
            # $ aws s3 cp s3://jlinoff-list-packages/python-3.7.3.txt /dev/stdout | \
            #      grep -v 'download: s3://' | \
            #      cat -n | \
            #      colorize -c bold+green '^.+==\d.*$'
            obj = boto3.resource('s3')
            path = f'{PYVER}.txt'
            obj.Object(S3_BUCKET, path).put(Body=content)
            print(f'Wrote package info to "s3://{S3_BUCKET}/{path}".')
        return make_status(200, body)
    
    
    def get_pkg_version(pkg: str) -> str:
        '''
        Figure out the package version.
    
        This is definitely a heuristic operation.
    
        The idea is to look for strings like __version__,
        version or VERSION.
        '''
        default_version = PYVER
        if pkg in ['sys', 'this', 'antigravity']:
            return default_version
        try:
            imp = importlib.import_module(pkg)
            versions = []
            for attr in dir(imp):
                if VERSION_PATTERN.match(attr):
                    obj = getattr(imp, attr)
                    if isinstance(obj, str):
                        versions.append(attr)
    
            versions = prune_versions(versions)
    
            if not versions:
                version = default_version
            elif len(versions) == 1:
                version = getattr(imp, versions[0])
            else:
                # multiple versions, pick the first one.
                version = getattr(imp, versions[0])
        except ModuleNotFoundError:
            version = 'error:module'
    
        return version
    
    
    def prune_versions(versions: list) -> list:
        '''
        Prune the versions.
        '''
        # In cases where there are multiple versions,
        # choose the one we want with precedence.
        if len(versions) > 1:
            done = False
            for preferred in ['__version__', 'version', 'VERSION']:
                for value in versions:
                    if preferred == value:
                        versions = [value]
                        done = True
                        break
                if done:
                    break
        return versions
    
    
    def make_status(code, msg='') -> dict:
        '''
        Make status codes in a uniform way.
        '''
        # This format was recommended by AWS.
        if not msg:
            try:
                msg = http.client.responses[code]
            except KeyError:
                msg = f'invalid key {code}'
    
        payload = {
            'isBase64Encoded': 'false',
            'statusCode': code,
            'headers': {'Content-Type': 'application/json'},
            'body': json.dumps(msg)
        }
        return payload
    
    
    if __name__ == '__main__':
        print(json.dumps(handler({}, {}), indent=2))

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

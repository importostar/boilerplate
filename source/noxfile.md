---
title: noxfile
date: 2020-05-07
---
Example Python program noxfile.py

## Modules

* import os
* import nox
* import py.path

## Methods

* def get_path(*names):
* def generate_plots(session):
* def update_requirements(session):

## Code

Python example

    # Licensed under the Apache License, Version 2.0 (the "License");
    # you may not use this file except in compliance with the License.
    # You may obtain a copy of the License at
    #
    #     https://www.apache.org/licenses/LICENSE-2.0
    #
    # Unless required by applicable law or agreed to in writing, software
    # distributed under the License is distributed on an "AS IS" BASIS,
    # WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    # See the License for the specific language governing permissions and
    # limitations under the License.
    
    """This is a configuration file for running ``nox`` on this project.
    
    To determine the supported actions run ``nox --list-sessions`` from the
    project root.
    """
    
    import os
    
    import nox
    import py.path
    
    
    nox.options.error_on_external_run = True
    NOX_DIR = os.path.abspath(os.path.dirname(__file__))
    DEFAULT_INTERPRETER = "3.7"
    
    
    def get_path(*names):
        return os.path.join(NOX_DIR, *names)
    
    
    @nox.session(py=DEFAULT_INTERPRETER)
    def generate_plots(session):
        """Generate plots showing the angle between vector pairs."""
        session.install("--requirement", get_path("requirements.txt"))
        # Make sure
        # - PDFs have deterministic ``CreationDate
        env = {"SOURCE_DATE_EPOCH": "0"}
        session.run("python", get_path("main.py"), env=env)
    
    
    @nox.session(py=DEFAULT_INTERPRETER)
    def update_requirements(session):
        """(Re)-generate the `requirements.txt` file."""
        if py.path.local.sysfind("git") is None:
            session.skip("`git` must be installed")
    
        # Install all dependencies.
        session.install("pip-tools")
    
        # Update the requirements file.
        in_name = "requirements.txt.in"
        txt_name = "requirements.txt"
        session.run("pip-compile", "--upgrade", "--output-file", txt_name, in_name)
        session.run("git", "add", txt_name, external=True)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

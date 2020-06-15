---
title: pipenv_virtualenv
date: 2020-05-07
---
Example Python program pipenv_virtualenv.py

## Modules

* import os
* import sys
* import logging
* import subprocess
* import sublime_plugin
* import Default as sublime_default
* from Virtualenv import virtualenv_lib as virtualenv
* from Virtualenv.commands import VirtualenvCommand

## Classes

* class PipenvVirtualenv(sublime_plugin.EventListener):
* Modified from <class 'Virtualenv.commands.VirtualenvExecCommand'>:
* class VirtualenvExecCommand(sublime_default.exec.ExecCommand, VirtualenvCommand):

## Methods

* def pipenv_venv(dir_path):
* def venv_interpreter(venv, raw_interpreter):
* def on_load_async(self, view):
* def on_post_save_async(self, view):
* def _update_venv(self, view):
* def run(self, **kwargs):
* def update_exec_kwargs(self, venv, **kwargs):

## Code

Python example

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    """
    Sublime Text 3 Pipenv virtualenv helper.
    
    1. Automatically find and set Pipenv virtualenv for each opened Python file.
    
    - It uses `pipenv --venv` command to find the virtualenv.
    - It will add a 'virtualenv' setting, which is the full path to the virtualenv,
    to the view's settings (view.settings()).
    - It will be triggered when files are loaded and saved.
    
    2. Automatically set virtualenv python interpreter for each file under
    virtualenv.
    
    - It will add a 'python_interpreter' setting, which is the full path to the
    virtualenv python interpreter, to the view's settings (view.settings()).
    Plugins like Anaconda and Flake8Lint can then use the 'python_interpreter'
    setting to get the correct virtualenv python interpreter to run their
    functions.
    
    3. Show each file's virtualenv name on the status bar.
    
    - The format is [venv_name].
    - It should be the first item on the status bar (STATUS_KEY = "000_venv_name").
    
    4. Modify and override Virtualenv package's virtualenv_exec command (Python
    Build System target).
    
    - Let virtualenv_exec command get virtualenv from the view's settings instead
    of the project's settings. Therefore, each view (file) can be run under its own
    virtualenv, instead that all files in the same window can only be run under one
    activated project virtualenv.
    
    Installation:
    - Save to your "/Sublime Text 3/Packages/User" directory.
    
    Dependencies:
    - Virtualenv package (https://github.com/AdrianLC/sublime-text-virtualenv)
    """
    
    import os
    import sys
    import logging
    import subprocess
    
    import sublime_plugin
    import Default as sublime_default
    
    from Virtualenv import virtualenv_lib as virtualenv
    from Virtualenv.commands import VirtualenvCommand
    
    
    STATUS_KEY = "000_venv_name"
    
    
    def pipenv_venv(dir_path):
        """Get Pipenv virtualenv path of given dir by `pipenv --venv` command."""
        env = os.environ
        env['LANG'] = "en_US.UTF-8"  # Set correct LANG to prevent Click error.
        try:
            cmd = ["pipenv", "--venv"]
            output = subprocess.check_output(cmd, cwd=dir_path, env=env)
            venv = output.decode('utf-8').strip()
        except subprocess.CalledProcessError:
            return None
        return venv or None
    
    
    def venv_interpreter(venv, raw_interpreter):
        """Get virturalenv python interpreter path.
    
        It should be {virturalenv}/bin/{interpreter}.
        """
        if not raw_interpreter:
            raw_interpreter = "python"
        if not raw_interpreter.startswith("python"):
            raw_interpreter = os.path.basename(raw_interpreter)
        return os.path.join(venv, "bin", raw_interpreter)
    
    
    class PipenvVirtualenv(sublime_plugin.EventListener):
        """EventListener for Pipenv virtualenv.
    
        Automatically find and set Pipenv virtualenv and virtualenv python
        interpreter when files are loaded and saved.
        """
    
        def on_load_async(self, view):
            """Update virturalenv when files are loaded."""
            self._update_venv(view)
    
        def on_post_save_async(self, view):
            """Update virturalenv when files are saved."""
            self._update_venv(view)
    
        def _update_venv(self, view):
            # Only run when it's a python file.
            try:
                source_syntax = view.scope_name(0).split()[0]
            except IndexError:
                return
            if not source_syntax.startswith('source.python'):
                return
    
            file_path = view.file_name()
            dir_path = os.path.dirname(file_path)
    
            # Get current file's virtualenv path by `pipenv --venv` command.
            venv = pipenv_venv(dir_path)
    
            if venv:
                # Add virtualenv setting to the view's settings.
                view.settings().set('virtualenv', venv)
                # Erase current python_interpreter setting from the view's settings
                # , in case it's already a view specific interpreter setting.
                view.settings().erase('python_interpreter')
                # Then, get python_interpreter setting from the view's settings.
                # Now, it should be defined syntax or project or global specific
                # interpreter setting.
                raw_interpreter = view.settings().get('python_interpreter')
                # Get virturalenv python interpreter path.
                python_interpreter = venv_interpreter(venv, raw_interpreter)
                # Add python_interpreter setting to the view's settings.
                view.settings().set('python_interpreter', python_interpreter)
    
                # Show virturalenv name on the status bar.
                venv_name = os.path.basename(venv)
                view.set_status(STATUS_KEY, "[{}]".format(venv_name))
            else:
                # Erase virtualenv setting from the view's settings.
                view.settings().erase('virtualenv')
                # Erase view specific interpreter setting from the view's settings.
                view.settings().erase('python_interpreter')
    
                # Erase virturalenv name from the status bar.
                view.erase_status(STATUS_KEY)
    
    
    """
    Override Virtualenv's virtualenv_exec command (Python Build System target).
    
    Modified from <class 'Virtualenv.commands.VirtualenvExecCommand'>:
    
    Let virtualenv_exec command get virtualenv from the view's settings instead
    of the project's settings. Therefore, each view (file) can be run under its own
    virtualenv, instead that all files in the same window can only be run under one
    activated project virtualenv.
    
    ~~~
    
    -        try:
    -            venv = self.get_virtualenv(validate=True, **kwargs)
    -        except InvalidVirtualenv as error:
    -            sublime.error_message(str(error) + " Execution cancelled!")
    -        else:
    -            if venv:
    -                kwargs = self.update_exec_kwargs(venv, **kwargs)
    -                logger.info("Command executed with virtualenv \"{}\".".format(venv))
    -            super(VirtualenvExecCommand, self).run(**kwargs)
    +        view = self.window.active_view()
    +        venv = view.settings().get('virtualenv', None)
    +        if venv:
    +            kwargs = self.update_exec_kwargs(venv, **kwargs)
    +            logger.info("Command executed with virtualenv \"{}\".".format(venv))
    +        super(VirtualenvExecCommand, self).run(**kwargs)
    """
    
    
    logger = logging.getLogger('Virtualenv.commands')
    
    
    class VirtualenvExecCommand(sublime_default.exec.ExecCommand, VirtualenvCommand):
    
        """Extends the default exec command adapting the build parameters."""
    
        def run(self, **kwargs):
            """Exec the command with virtualenv.
    
            If a virtualenv is active and valid update the build parameters
            as needed and call the built-in command.
    
            Else, if no virtualenv is active, do nothing and call the built-in
            command.
            """
            view = self.window.active_view()
            venv = view.settings().get('virtualenv', None)
            if venv:
                kwargs = self.update_exec_kwargs(venv, **kwargs)
                logger.info("Command executed with virtualenv \"{}\".".format(venv))
            super(VirtualenvExecCommand, self).run(**kwargs)
    
        def update_exec_kwargs(self, venv, **kwargs):
            """Modify exec kwargs to make use of the virtualenv."""
            postactivate = virtualenv.activate(venv)
            kwargs['path'] = postactivate['path']
            kwargs['env'] = dict(kwargs.get('env', {}), **postactivate['env'])
            kwargs['env'].pop('PYTHONHOME', None)
            # On OS X, avoid being run in a login shell, to preserve the virtualenv-ized PATH
            if sys.platform == 'darwin' and 'shell_cmd' in kwargs:
                kwargs['cmd'] = ['/bin/bash', '-c', kwargs['shell_cmd']]
                del kwargs['shell_cmd']
            return kwargs
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: leaderkey
date: 2020-05-07
---
Example Python program leaderkey.py

## Modules

* from enum import Enum
* import os
* import string
* import sys
* import tkinter

## Classes

* class UIMode:
* class LeaderGroup:
* class LeaderPrompt:
* class LeaderAction:
* class UI:

## Methods

* def execfile(filename, globals=None, locals=None):
* def __init__(self):
* def add(self, prefix, hint, leader):
* def prepare(self, ui, variables):
* def execute(self, user_input, variables):
* def hint(self):
* def __init__(self, hint):
* def attach(self, after):
* def prepare(self, ui, variables):
* def execute(self, user_input, variables):
* def hint(self):
* def __init__(self, command):
* def substitute(self, template, variables):
* def prepare(self, ui, variables):
* def execute(self, user_input, variables):
* def hint(self):
* def __init__(self, root_leader):
* def run(self):
* def on_keypress(self, event):
* def on_entry_done(self, event):
* def update_leader(self, user_input):
* def change_mode(self, mode, is_init=False):
* def add_hint(self, hint):
* def clear_hints(self):
* def group():
* def prompt(hint, followup):
* def action(command):

## Code

Python tkinter example

    #!/usr/bin/python3
    #
    # Command Line
    # ------------
    # ``python3 leaderkey.py CONFIG-FIlE``
    #
    # Configuration format
    # --------------------
    #
    # A leaderkey configuration is a normal Python file, with the following
    # additional operations available in the global scope:
    #
    # - ``g = group()`` creates a new leader group, to which other groups
    #   can be attached via ``g.add(<prefix>, <hint>, <command>)``. A
    #   command can be another group, a prompt or an action. A string can
    #   also be used as a short-hand for an action.
    #
    # - ``p = prompt(<hint>, <command>)`` creates a new prompt, which asks
    #   the user for a value and then chains to the next command.
    #
    # - ``a = action(<cmdline>)`` executes a command via ``os.system()``. Note
    #   that this includes a special escape syntax for referring to prompt
    #   arguments using the ``%`` character; for example ``action(firefox %1)``
    #   can be used to visit the URL given by the outer-most prompt. Currently,
    #   only 9 prompts can be accessed (``%1`` through ``%9``) with ``%%``
    #   serving as a literal ``%``.
    #
    # The root element must be a global variable called **ROOT**.
    #
    # For example, here is a simple configuration using all of the
    # available options::
    #
    #     browsers = group()
    #     browsers.add('f', 'firefox homepage', 'firefox')
    #     browsers.add('F', 'firefox w/url', prompt('url', 'firefox %1'))
    #
    #     editors = group()
    #     editors.add('e', 'emacs', action('emacs'))
    #
    #     java = group()
    #     java.add('i', 'idea', 'idea')
    #     java.add('e', 'eclipse', 'eclipse')
    #     editors.add('j', 'java', java)
    #
    #     ROOT = group()
    #     ROOT.add('b', 'browsers', browsers)
    #     ROOT.add('e', 'editors', editors)
    #
    # This could lead to the following interactions:
    #
    # - ``b f`` would open Firefox to your homepage
    # - ``b F https://www.google.com <RETURN>`` would open Firefox to Google
    # - ``e j e`` would open Eclipse
    from enum import Enum
    import os
    import string
    import sys
    import tkinter
    
    def execfile(filename, globals=None, locals=None):
        """
        Executes the contents of the file inline - arguments are same as exec,
        except that a path is given instead of code.
        """
        with open(filename) as script_file:        
            exec(script_file.read(), globals, locals)        
    
    class UIMode:
        WAIT_FOR_LEADER = 1
        WAIT_FOR_PROMPT = 2
        DONE = 3
    
    class LeaderGroup:
        def __init__(self):
            self.prefixes = {}
            self.hints = {}
    
        def add(self, prefix, hint, leader):
            """
            Binds a subleader's prefix to the subleader, and a hint to display.
            """
            if isinstance(leader, str):
                # This lets the configuration file be a bit lazier, e.g.
                #  
                #  group().add('x', 'xterm', 'xterm')
                #
                # Instead of:
                #
                #  group().add('x', 'xterm', action('xterm'))
                leader = LeaderAction(leader)
    
            self.prefixes[prefix] = leader
            self.hints[prefix] = hint
    
        def prepare(self, ui, variables):
            """
            Pushes the subleader's hints to the UI and prepares it to dispatch
            on them.
            """
            ui.clear_hints()
            for prefix, hint in sorted(self.hints.items()):
                ui.add_hint(prefix + ' => ' + hint)
    
            return UIMode.WAIT_FOR_LEADER
    
        def execute(self, user_input, variables):
            """
            Finds the next leader for the key the user pressed.
            """
            return self.prefixes.get(user_input, None)
    
        def hint(self):
            """
            Returns an aggregate hint for all subleaders.
            """
            return ', '.join(sorted(self.hints.values()))
    
    class LeaderPrompt:
        def __init__(self, hint):
            self._hint = hint
            self.next_leader = None
    
        def attach(self, after):
            """
            Attaches another leader to occur after this one.
            """
            if isinstance(after, str):
                # See LeaderGroup.add for the rationale
                after = LeaderAction(after)
    
            self.next_leader = after
    
        def prepare(self, ui, variables):
            """
            Pushes the subleader's hints to the UI and prepares it to dispatch
            on them.
            """
            ui.clear_hints()
            ui.add_hint(self._hint)
            return UIMode.WAIT_FOR_PROMPT
    
        def execute(self, user_input, variables):
            """
            Finds the next leader for the key the user pressed.
            """
            variables.append(user_input)
            return self.next_leader
    
        def hint(self):
            """
            Returns the hint for this prompt.
            """
            return self._hint
    
    class LeaderAction:
        def __init__(self, command):
            self.command = command
    
        def substitute(self, template, variables):
            """
            Substitutes in the list of variables to the command template.
            """
            buffer = []
            escape = True
            for char in template:
                if escape:
                    if char in '123456789':
                        try:
                            buffer.append(variables[int(char) - 1])
                        except IndexError:
                            buffer.append('%' + char)
                    else:
                        buffer.append(char)
                    escape = False
                elif char == '%':
                    escape = True
                else:
                     buffer.append(char)
    
            if escape:
                buffer.append('%')
    
            return ''.join(buffer)
    
        def prepare(self, ui, variables):
            """
            Executes the subcommand and tells the UI to exit.
            """
            full_command = self.substitute(self.command, variables)
    
            pid = os.fork()
            if pid == 0:
                os.setsid()
                child_pid = os.fork()
                if child_pid != 0:
                    sys.exit(0)
    
                retcode = os.system(full_command)
                os._exit(retcode)
            else:
                return UIMode.DONE
    
        def execute(self, user_input, variables):
            """
            This should never be executed, because the UI should not be running
            after LeaderAction.prepare returns UIMode.DONE
            """
            assert False
    
        def hint(self):
            """
            Returns the command as the hint; the user won't see this, so its
            real contents don't matter.
            """
            return self.command
    
    class UI:
        def __init__(self, root_leader):
            self.current_leader = root_leader
            self.waiting_for_keypress = True
            self.variables = []
            self.history = []
    
            self.window = tkinter.Tk()
            self.leader_history = tkinter.Label(self.window)
            self.hints = tkinter.Listbox(self.window)
            self.prompt = tkinter.Entry(self.window)
    
            self.window.bind('<Key>', self.on_keypress)
            self.prompt.bind('<Return>', self.on_entry_done)
    
            self.current_leader.prepare(self, self.variables)
            self.change_mode(UIMode.WAIT_FOR_LEADER, is_init=True)
    
        def run(self):
            """
            Runs the Tk event loop until the user exits.
            """
            self.window.mainloop()
    
        def on_keypress(self, event):
            """
            Accepts a key press and redirects it to the appropriate leader.
            """
            if event.char == '':
                # Modifier keys don't generate characters
                return
    
            if event.keysym == 'Escape':
                self.change_mode(UIMode.DONE)
            elif self.waiting_for_keypress:
                self.history.append(event.char)
                self.leader_history.config(text=' '.join(self.history))
                self.update_leader(event.char)
    
        def on_entry_done(self, event):
            """
            Accepts input from the entry and passes it onto the next leader.
            """
            self.update_leader(self.prompt.get())
    
        def update_leader(self, user_input):
            """
            Executes the leader, and replaces the current one with the leader
            generated.
            """
            self.current_leader = self.current_leader.execute(user_input, self.variables)
    
            if self.current_leader is None:
                self.change_mode(UIMode.DONE)
            else:
                new_mode = self.current_leader.prepare(self, self.variables)
                self.change_mode(new_mode)
    
        def change_mode(self, mode, is_init=False):
            """
            Reconfigures the UI to match the given mode.
            """
            if mode == UIMode.WAIT_FOR_LEADER:
                # This is the default mode - do nothing unless we're just 
                # starting up
                self.waiting_for_keypress = True
    
                if is_init:
                    self.leader_history.pack()
                    self.hints.pack()
            elif mode == UIMode.WAIT_FOR_PROMPT:
                self.waiting_for_keypress = False
                self.prompt.pack()
                self.prompt.focus_set()
            elif mode == UIMode.DONE:
                self.window.destroy()
    
        def add_hint(self, hint):
            """
            Add a new hint to the hint list.
            """
            self.hints.insert('end', hint)
    
        def clear_hints(self):
            """
            Removes all hints from the hint list.
            """
            self.hints.delete(0, 'end')
    
    def group():
        """
        Configuration wrapper around LeaderGroup
        """
        return LeaderGroup()
    
    def prompt(hint, followup):
        """
        Configuration wrapper around LeaderPrompt
        """
        if isinstance(followup, str):
            followup = action(followup)
    
        prompt = LeaderPrompt(hint)
        prompt.attach(followup)
        return prompt
    
    def action(command):
        """
        Configuration wrapper around LeaderAction
        """
        return LeaderAction(command)
    
    if __name__ == '__main__':
        config = {
            'group': group,
            'prompt': prompt,
            'action': action
        }
        execfile(sys.argv[1], config)
    
        ui = UI(config['ROOT'])
        ui.run()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

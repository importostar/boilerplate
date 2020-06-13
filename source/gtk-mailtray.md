---
title: gtk mailtray
date: 2020-05-07
---
Example Python program gtk-mailtray.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import gi
* from gi.repository import Gtk
* from signal import signal, SIGUSR1, SIGUSR2
* import os

## Classes

* class MailTray:

## Methods

* def __init__(self):
* def check_new(self, _=None):
* def state_idle(self, *args):
* def state_receiving(self, *args):
* def cleanup(self, _=None):
* def popup_menu_cb(self, widget, button, time, data=None):

## Code

Python example

    #!/usr/bin/python3
    
    # System tray icon displaying email syncing state.
    # Tell the tray that email is syncing:
    #   kill -USR1 $(cat $XDG_RUNTIME_DIR/mailtray.pid)
    # Sync has completed and recalculate new emails:
    #   kill -USR2 $(cat $XDG_RUNTIME_DIR/mailtray.pid)
    #
    # However, the `Gtk.StatusIcon` used in this script has been deprecated and I haven't found a
    # replacement.
    
    import gi
    gi.require_version('Gtk', '3.0')
    from gi.repository import Gtk
    
    from signal import signal, SIGUSR1, SIGUSR2
    import os
    
    MAILDIR = os.environ.get('MAILDIR', os.path.expandvars("$HOME/Mail"))
    
    
    class MailTray:
        def __init__(self):
            self.icon = Gtk.StatusIcon()
            self.menu = Gtk.Menu()
            cn = Gtk.MenuItem.new_with_label('Update count')
            cn.connect('activate', self.state_idle)
            self.menu.append(cn)
            quit = Gtk.MenuItem.new_with_label('Quit')
            quit.connect('activate', self.cleanup)
            self.menu.append(quit)
            self.icon.connect('popup-menu', self.popup_menu_cb)
            self.new_count = {}
            self.state_idle()
    
            try:
                self.pidfile = os.path.join(os.environ['XDG_RUNTIME_DIR'], 'mailtray.pid')
            except KeyError:
                print('XDG_RUNTIME_DIR is not set')
            with open(self.pidfile, 'w') as f:
                f.write(str(os.getpid()))
    
            signal(SIGUSR1, self.state_receiving)
            signal(SIGUSR2, self.state_idle)
    
        def check_new(self, _=None):
            self.new_count = {
                acc: len(list(filter(lambda x: x, os.popen(
                    f"""sh -c 'find "{MAILDIR}/{acc}/Inbox/new/" -type f -print0'"""
                ).read().split('\0'))))
                for acc in filter(lambda s: not s.startswith('.'), os.listdir(MAILDIR))
            }
    
        def state_idle(self, *args):
            self.check_new()
            msg = ', '.join(f'{a} ({n})' for a, n in
                            filter(lambda it: it[1] != 0, self.new_count.items()))
            if msg:
                self.icon.set_tooltip_text(msg)
                self.icon.set_from_icon_name('mail_new')
            else:
                self.icon.set_tooltip_text('Mail')
                self.icon.set_from_icon_name('mail_generic')
    
        def state_receiving(self, *args):
            self.icon.set_tooltip_text('Mail')
            self.icon.set_from_icon_name('mail-send-receive')
    
        def cleanup(self, _=None):
            try:
                os.remove(self.pidfile)
            except Exception:
                pass
            Gtk.main_quit()
    
        def popup_menu_cb(self, widget, button, time, data=None):
            self.menu.show_all()
            self.menu.popup(None, None, Gtk.StatusIcon.position_menu, self.icon, button, time)
    
    
    if __name__ == '__main__':
        MailTray()
        Gtk.main()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

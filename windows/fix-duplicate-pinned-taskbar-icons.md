# Fix Duplicate Icons in Windows 10 Taskbar

When pinning a program to the Win 10 taskbar, sometimes running the program
via the pinned shortcut will lead to giving the run instance a new taskbar entry.
Seems to happen a lot for mintty for whatever reason.

This is annoying as fuck, so here's how to fix it:

- close all instances, unpin from taskbar
- open `%AppData%\Microsoft\Internet Explorer\Quick Launch\User Pinned\TaskBar\`
- delete any existing shortcut to the affected program there
- create a fresh new shortcut (adjust command line if neccessary)
- run program from the created shortcut, pin to taskbar
- note that this will create *a new shortcut* in
`%AppData%\Microsoft\Internet Explorer\Quick Launch\User Pinned\TaskBar\`
- you can either ignore that, or clean up:
  - delete the *original* shortcut (this is important!)
  - rename the copy (propably named "foo(2)") back to the old name (or anything) - this will not break the pinned taskbar entry

Sauce:
https://www.ghacks.net/2015/08/04/fix-duplicate-icon-issues-on-the-windows-taskbar/

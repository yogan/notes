# Auto Run Programs

To automatically start some programs that are already pinned to
the Windows taskbar, you can just copy the shortcuts.

* `explorer "%APPDATA%\Microsoft\Internet Explorer\Quick Launch\User Pinned\TaskBar"`
* `explorer "%APPDATA%\Microsoft\Windows\Start Menu\Programs\Startup"`
* copy everything that shall be started after logon

Some applications (e.g. Spotify) have there own auto startup mechanism.
Sysinternals Autoruns (`choco install autoruns`) can be used to check those.

# Setting up a fresh Windows machine

## Essentials

- [WinGet](https://docs.microsoft.com/en-us/windows/package-manager/) - grab and install
  `*.appxbundle` from [GitHub releases](https://github.com/microsoft/winget-cli/releases)
- [Google Drive](https://www.google.com/drive/download/) - `winget install Google.BackupAndSync`
- [PowerToys](https://github.com/microsoft/PowerToys) - `winget install powertoys`
- [Windows Terminal](https://github.com/microsoft/terminal) - `winget install Microsoft.WindowsTerminalPreview`
- [KeePass](http://keepass.info/) - `winget install keepass`
- [Chrome](https://www.google.de/intl/de/chrome/browser/desktop/index.html) -
  `winget install Google.Chrome`

## Keyboard

- Use [*Keyboard Manager*](https://aka.ms/PowerToysOverview_KeyboardManager) of *PowerToys* to remap some keys:
  - map `<CapsLock>` → `<Ctrl>`
  - swap `<Esc>` ↔ `<~>`
  - for reference: used to do this with [SharpKeys](https://sharpkeys.codeplex.com),
    but PowerToys can now do the same thing, and even without forcing to sign-out
- [WinCompose](https://github.com/SamHocevar/wincompose) - `choco install wincompose`
  - symlink `WinCompose.XCompose` to `.XCompose` in `%userprofile%` (details how
    to symlink are at the top of `WinCompose.XCompose` itself)
  - use a env clone in Windows for this; do not link to env within WSL!

## System Tools

### Link Shell Extension

[Link Shell
Extension](http://schinagl.priv.at/nt/hardlinkshellext/hardlinkshellext.html) -
`choco install LinkShellExtension` - to create symlinks, hardlinks, junctions,
etc.

### clink

[clink](https://mridgers.github.io/clink/) - `winget  install clink` -
readline/history for `cmd.exe`

- symlink `env/clink/settings` to `C:\Users\<USERNAME>\AppData\Local\clink\`
- create *hardlink* to `env/.inputrc` in `C:\Users\<USERNAME>\`
- rename hardlinked `.inputrc` to `_inputrc`

### Miscellaneous

- [Process
  Explorer](https://technet.microsoft.com/en-us/sysinternals/bb896653.aspx) -
  `choco install procexp`
- [Autoruns](https://technet.microsoft.com/en-us/sysinternals/bb963902.aspx) -
  `choco install AutoRuns`
- [Rufus](http://rufus.akeo.ie) create bootable USB drives from `.iso` images
  (like with `dd` on Linux) `choco install rufus` (note: `rufus.exe` can be
  found in `C:\ProgramData\chocolatey\bin`, it does not get added to the start
  menu automatically by choco)

## Applications

### Vim

- `choco install vim`
- create *hardlink* to `env/.vimrc` in `$HOME` (`c:/user/foo/`)
- rename hardlinked `.vimrc` to `_vimrc`
- make *junction* of `env/.vim/` to `c:\Program Files\vim\`
- rename `.vim` to `vimfiles` (remove old one there)

### Spotify

- [Spotify](https://www.spotify.com/de/download/windows/)
  *(self-updating, so use installer instead of choco)*
- [Toastify](https://github.com/aleab/toastify/releases) - global
  keyboard shortcuts and notifications

### Graphics/Viewers

- [SumatraPDF](http://www.sumatrapdfreader.org/free-pdf-reader.html) -
  `choco install sumatrapdf`
- [Paint.NET](http://www.getpaint.net) - `choco install paint.net`
- [ScreenToGif](http://www.screentogif.com/) - `choco install screentogif`
- also see [tools/graphics page](../tools/graphics.md)

## WSL

See [Windows Subsystem for Linux (WSL)](wsl.md).

### Clone git Repos

To enable working with both Linux (WSL) and Windows programs on the files in my
git repositories, they have to be cloned to a Windows path. Cloning and other
git operations can be done straight from a WSL shell with WSL git.

```sh
cd winhome
git clone ssh://zogan.de/~yogan/git/priv/env
git clone ssh://zogan.de/~yogan/git/priv/docs
cd ; ln -s winhome/env ; ln -s winhome/docs
```

### Useful WSL Utilities

- [xclip-xsel-WSL](https://github.com/Konfekt/xclip-xsel-WSL) provides `xclip`
  and `xsel` in WSL so that you can access the Windows clipboard from the
  command line

## Development

### VS Code

- `choco install VisualStudioCode`
- be sure to have Explorer integration checked (if not, run installer again
  later)

For initial setup, get user settings from gist:

- add the [Settings
  Sync](https://marketplace.visualstudio.com/items?itemName=Shan.code-settings-sync)
  extension
- `<Ctrl><Shift><p>` → `Preferences: Open User Settings`
  - add `"sync.gist": "ae3bdfbb98c2054b242e1e0361628bfb"`
  - remove all other `sync.*` settings
- `<Ctrl><Shift><p>` → `Sync: Download settings`

Settings are stored in `%APPDATA%\Code\User\`.

**TODO:** *figure out how this fscking `syncLocalSettings.json` works*

## References

- A good starting point for setting up a dev environment on Windows is
  *[Windows development environment](https://docs.microsoft.com/en-us/windows/dev-environment/)*
  on *[Microsoft Docs](https://docs.microsoft.com/en-us/)*.
- [SoCraTes 2016 Windows Tools Session Notes](https://blog.sandra-parsick.de/2016/09/20/summary-of-socrates-2016-session-hey-dude-where-is-my-tool-chain-working-on-windows-as-a-linux-user-aka-lets-talk-about-windows/)

## Package Managers

### Windows Package Manager aka winget (preview)

The
[Windows Package Manager](https://docs.microsoft.com/en-us/windows/package-manager/)
was announced at MS Build 2020 and is currently in preview. It could potentially
replace Chocolatey in the long run. On Windows 10 Insider, `winget` is already
available. For stable Windows 10, the quickest way to get it is to grab the
latest [release from GitHub](https://github.com/microsoft/winget-cli/releases)
(it's part of *AppInstaller*, so download the
`Microsoft.DesktopAppInstaller_GIBBERISH.appxbundle` thingy and run that,
it's fine).

For [winget](https://docs.microsoft.com/en-us/windows/package-manager/winget/)
usage information, just call `winget` without any arguments. There is `search`
and `install`, as you would expect, but currently there does not seem to be an
`update`.

### Chocolatey

#### First Time Setup

- [install Chocolatey](https://chocolatey.org/install) as described (from Admin
  `cmd` or `PowerShell`)
- `choco` should be in `%PATH%` after installation
  - ProTip™: use `which` npm package (`npm install -g which`)
- Run all future `choco` commands as admin
- `choco feature enable -n=allowGlobalConfirmation`

#### Usage

It makes sense to always use an elevated (Admin) `cmd` or `PowerShell` to work
with `choco` (as we are installing software, this is perfectly fine.)

To install something new:

- `choco search foo`
- `choco install foo`

List and upgrade locally installed packages.

- `choco list -l`
- `choco upgrade all`

## TODO

- [ ] evaluate [Boxstarter](http://boxstarter.org/) (see blog post by jsfraz:
  [Setting Up a Windows Machine in a Reproducible
  Way](https://blog.jessfraz.com/post/windows-for-linux-nerds/#setting-up-a-windows-machine-in-a-reproducible-way))

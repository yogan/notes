# Windows Subsystem for Linux (WSL)

## Resources
* [List blog posts and Channel 9 videos of WSL internals](https://blogs.msdn.microsoft.com/commandline/learn-about-bash-on-windows-subsystem-for-linux/)
* [Microsoft/BashOnWindows GitHub Issue Tracker](https://github.com/microsoft/bashonwindows)
* [List of programs that work on WSL](https://github.com/ethanhs/WSL-Programs) / [Can I Subsystem It?](https://github.com/davatron5000/can-i-subsystem-it)
* [Release Notes](https://msdn.microsoft.com/en-us/commandline/wsl/release_notes) (updated with newer builds)

## Install
* [Installation Guide](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide)
* TL;DR:
  * enable Developer Mode (Settings → Update and Security → For developers)
  * turn it on: Start → "turn feat" → "Turn Windows features on or off" → [x] WSL
  * reboot when prompted
  * `cmd` → `bash` → let installer run
  * `cmd` → `bash` → create user/password

## Upgrade
Initial WSL (released with Win 10 Annivery Update / v1607) shipped with Ubuntu 14.04 LTS (Trusty).
With [WSL Build 14951](https://msdn.microsoft.com/en-us/commandline/wsl/release_notes#build-14951)
(which itself is available since Windows 10 Creators Update / v1703)
Ubuntu 16.04 LTS (Xenial) is [supported](https://blogs.msdn.microsoft.com/commandline/2016/10/19/wsl-adds-ubuntu-16-04-xenial-support/),
but not automatically upgraded.

To check versions:
* Windows: `winver.exe`
* WSL/Ubuntu: `lsb_release -a`

To upgrade an existing 14.04, you can either:

* uninstall/reinstall: `lxrun /uninstall /full /y` / `lxrun /install` (from `cmd` or PowerShell)
* upgrade in place: `sudo do-release-upgrade` (inside a running WSL shell)

The later seems to work fine, just like upgrading a "real" Ubuntu/Debian installation. After the upgrade, a Windows reboot is needed.

## Post-Install
* sudo apt-get update && sudo apt-get dist-upgrade
* Make sure that the `umask` is set to `022`, which is not the case in the initial `bash` instance, otherwise cloned git repos (and everything else) have fucked up file/dir permissions!
  * set in running shell with `umask 022`
  * also add to the top of the shipped WSL version of `~/.bashrc`
  * later in `fish` everything will be fine, as this is done by my config (`.config/fish/conf.d/env.fish`)
* `git clone ssh://yogan@zogan.de/~yogan/git/priv/env` *(actually do this twice: once in the WSL home, and once in Windows home; reason: r/w from outside of WSL should not be done, see section "Interoperability", but to keep permissions and special file types like symlinks in the Linux world, just symlinking out of the WSL filesystem is also not possible)*
* `./env/bin/symlink-env.sh`
* `ssh-keygen`

## Add mintty/wsltty as Terminal

**TODO:**
After installation of Windows Fall Creators Update (v1709), wsl comes with a `wsl.exe` that respects shell entries from `/etc/passwd`, so `chsh` should work. See if it really does, and replace the manual launch of fish below.
Also see [GH Issue 2199](https://github.com/Microsoft/BashOnWindows/issues/2199) and [GH Issue 2510](https://github.com/Microsoft/BashOnWindows/issues/2510).

* [wsltty@GitHub](https://github.com/mintty/wsltty), use installer
* symlink `env/.minttyrc` to `%APPDATA%\wsltty\config`
  * delete shipped `%APPDATA%\wsltty\config` file
  * use `env` git from Windows home; symlink with Explorer/ShellExt
  * rename `.minttyrc` symlink to `config`
* copy *"WSL ~ in Mintty"* shortcut in `%APPDATA%\Microsoft\Windows\Start Menu\Programs\WSLtty`, rename to *"WSL fish"*
* adapt target of shortcut to use `fish` instead of `bash`:
  * `%LOCALAPPDATA%\wsltty\bin\mintty.exe --wsl -h err --configdir="%APPDATA%\wsltty" `*`-o FontHeight=12`*` /bin/wslbridge -C~ -t /usr/local/bin/fish`
  * `-o LOCALE=C -o Charset=UTF-8` from shipped wsltty shortcut can be removed, they are present in my symlinked `.minttyrc` anyway
  * `-o FontHeight `*`NUM`* can be added when needed to override the value from the config file
* font: install "DejaVu Sans Mono Nerd Font" from [NerdFonts repo](https://github.com/ryanoasis/nerd-fonts/releases) (unzip, install `"* Mono Windows Compatible.ttf"`)
* eye candy: use icon from `env/icons/fish-terminal.ico`

## fish Shell

### Build and Install from Source
* `git clone git://github.com/fish-shell/fish-shell.git && cd fish-shell`
* `sudo apt install autoconf automake build-essential libncurses5-dev gettext doxygen`
* `autoreconf --no-recursive`
* `./configure` *(normally I would add `--prefix=$HOME/local`, but for WSL it's fine to install globally)*
* `make -j && sudo make install`
* *adding to `/etc/shells` and `chsh` are not needed/don't work on WSL*

### Setup oh-my-fish
* `curl -L https://get.oh-my.fish | fish` (if you like to live dangerously, or [download and check](https://github.com/oh-my-fish/oh-my-fish#installation) the installer first)
* `omf install` (to get theme)
* `omf reload`

### Setup fzf
* `git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf`
* `~/.fzf/install`
* answer setup questions:
  * `Do you want to enable fuzzy auto-completion?` **`y`**
  * `Do you want to enable key bindings?`  **`y`**
  * `Do you want to update your shell configuration files?` **`n`**
* `omf reload`

### $PATH / $fish_user_paths
Path things are a bit weird in fish. You can add paths to a universal variable `fish_user_paths`,
which then magically is persisted on the local machine, and also prepended to `PATH`. This actually
works better then expected. I have two little convenience functions `path` (to print the values of
the two variables) and `add_path` (to add e.g. `~/bin`, `~/.fzf/bin`, etc.)


## Interoperability

### Filesystem

The WSL filesystem root is located in `%LOCALAPPDATA%\LXSS` and
[*should not* be modified](https://blogs.msdn.microsoft.com/commandline/2016/11/17/do-not-change-linux-files-using-windows-apps-and-tools/)
by Windows applications. The Windows filesystems ("drives") are mounted below
`/mnt/{c,d,...}` under WSL and *can* be modified from Linux applications.

So for any shared data it is good practice to place them in some Windows directory, e.g. somewhere
below the Windows user home (`%userprofile%` → `C:\Users\<foo>`) access them from WSL via a symlink,
e.g. `ln -s /mnt/c/Users/fbr/ winhome`.

### Launching Windows Applications

Since [build 14965](https://msdn.microsoft.com/en-us/commandline/wsl/release_notes#build-14965),
Windows applications can be easily launched from a WSL shell, as the NT user path is by default
appended to the Linux `$PATH`. Just try something like `notepad.exe` or even go nuts and do `cmd.exe`.

The current (Linux) working directory is translated and passed to the Windows application, as long as
it is something below `/mnt/`; otherwise a warning will be printed. So you can e.g. start VS Code in
the current directory with `code .`

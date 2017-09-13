# Windows Subsystem for Linux (WSL)
**(aka Bash on Ubuntu on Windows)**

Ongoing installation/setup notes.

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
Ubuntu 16.06 LTS (Xenial) is [supported](https://blogs.msdn.microsoft.com/commandline/2016/10/19/wsl-adds-ubuntu-16-04-xenial-support/),
but not automatically upgraded.

To upgrade an existing 14.04, you can either:

* uninstall/reinstall: `lxrun /uninstall /full /y` / `lxrun /install` (from `cmd` or PowerShell)
* upgrade in place: `sudo do-release-upgrade` (inside a running WSL shell)

The later seems to work fine, just like upgrading a "real" Ubuntu/Debian installation. After the upgrade, a Windows reboot is needed.

## Post-Install
* `sudo apt-get dist-upgrade`
* `sudo install git zsh`
* `ssh-keygen ; eval $(ssh-agent) ; ssh-add`
* Make sure that the `umask` is set to `022` (should be done by `zsh`/`fish` configs), otherwise cloned git repos (and everything else) have fucked up file/dir permissions. When cloning initial env with `bash`, either set `umask` manually or just add it to the (default WSL) `.bashrc`.
* `git clone ssh://yogan@zogan.de/~yogan/git/priv/env`
* `./env/bin/symlink-env.sh`

## Add mintty as Terminal
* [wsltty@GitHub](https://github.com/mintty/wsltty)
* symlink `env/.minttyrc` to `%APPDATA%\mintty\config` (rename `.minttyrc` to `config`)
* copy shortcut in `%APPDATA%\Microsoft\Windows\Start Menu\Programs\WSLtty`
* adapt to use `zsh` instead of `bash`: `%LOCALAPPDATA%\wsltty\bin\mintty.exe -t "wsl/zsh" --wsl /bin/wslbridge -C~ -t /bin/zsh --login`

## fish

### Build and Install from Source
* `git clone git://github.com/fish-shell/fish-shell.git`
* `autoreconf --no-recursive`
* `./configure` *(normally I would add `--prefix=$HOME/local`, but for WSL it's fine to install globally)*
* `make -j && sudo make install`
* *adding to `/etc/shells` and `chsh` are not needed/don't work on WSL*

### Starting with mintty
* like for `zsh` above; just change param given to `wslbridge` to `/usr/local/bin/fish`

### Setup oh-my-fish
* `curl -L https://get.oh-my.fish | fish` (if you like to live dangerously, or [download and check](https://github.com/oh-my-fish/oh-my-fish#installation) the installer first)
* `omf install` (to get theme)
* `omf reload`

## zsh
* workaround to make default shell (`chsh` does not help):
  * launch from `mintty` via `wslbridge` (see above)
  * add `export SHELL=/bin/zsh` to `~/.zshenv`

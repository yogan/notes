# Windows Subsystem for Linux (WSL)

## Resources

* [List blog posts and Channel 9 videos of WSL
  internals](https://blogs.msdn.microsoft.com/commandline/learn-about-bash-on-windows-subsystem-for-linux/)
* [Microsoft/BashOnWindows GitHub Issue
  Tracker](https://github.com/microsoft/bashonwindows)
* [List of programs that work on WSL](https://github.com/ethanhs/WSL-Programs) /
  [Can I Subsystem It?](https://github.com/davatron5000/can-i-subsystem-it)
* [Release
  Notes](https://msdn.microsoft.com/en-us/commandline/wsl/release_notes)
  (updated with newer builds)

## Install

* [Installation
  Guide](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide)
* TL;DR:
  * enable Developer Mode (Settings → Update and Security → For developers)
  * turn it on: Start → "turn feat" → "Turn Windows features on or off"
    → [x] WSL
  * reboot when prompted
  * download a [Distro from the Windows Store](https://docs.microsoft.com/en-us/windows/wsl/install-win10#install-your-linux-distribution-of-choice)
  * launch Distro, wait for install to finish, create Linux user/password

## Post-Install

* `sudo apt-get update && sudo apt-get dist-upgrade`
* Make sure that the `umask` is set to `022`, which is not the case in the
  initial `bash` instance, otherwise cloned git repos (and everything else) have
  fucked up file/dir permissions!
  * set in running shell with `umask 022`
  * also add to the top of the shipped WSL version of `~/.bashrc`
  * later in `fish` everything will be fine, as this is done by my config (`.config/fish/conf.d/env.fish`)
* `git clone ssh://yogan@zogan.de/~yogan/git/priv/env` *(actually do this twice:
  once in the WSL home, and once in Windows home; reason: r/w from outside of
  WSL should not be done, see section "Interoperability", but to keep
  permissions and special file types like symlinks in the Linux world, just
  symlinking out of the WSL filesystem is also not possible)*
* `./env/bin/symlink-env.sh`
* `ssh-keygen`
* build and install [fish](../linux/fish.md) (see instructions on [its own page](../linux/fish.md))

## Host Names for WSL2 Instances

WSL2 are more like VMs (compared to WSL1), so each instance will also have its
own (usually dynamic) IP address. To make it easier to access WSL2 hosts from
the outside, you can use [go-wsl2-host](https://github.com/shayne/go-wsl2-host).
This runs as a system service, and updates Windows' `/etc/hosts` file, so that
you can e.g. use `ubuntu2004.wsl` to access a Ubuntu WSL2 host with that name.

Note that you need to set up this tool as a system service, which mean that you
have to provide your user credentials to it, and make sure that your
[policies are configured so that your user can log on as a system
service](https://github.com/shayne/go-wsl2-host/issues/10#issuecomment-597399481):

> Local Security Policy > Local Policies > User Rights Assignment > Log on as a service

## Interoperability

### Filesystem

Since Win 10 1903, you
[can access Linux file from Windows](https://devblogs.microsoft.com/commandline/whats-new-for-wsl-in-windows-10-version-1903/)
via a 9P based file server, which makes the files of a WSL distro available
under `\\wsl$\DISTRO\…`.

The
[old warning](https://blogs.msdn.microsoft.com/commandline/2016/11/17/do-not-change-linux-files-using-windows-apps-and-tools/)
that you should never access Linux files via AppData (`%LOCALAPPDATA%\LXSS`)
however, still applies.

It might still be convenient to place some symlinks to Windows directories,
e.g. `ln -s /mnt/c/Users/fbr/ winhome`.

### Ownership and Permissions

By default, the Windows filesystems mounted via DrvFs shows all files with
`root:root` ownership. Permission bits are derived from the Windows FS
attributes, but cannot be changed with `chmod`. Insider build 17063 introduces
some enhancements, and limited support for `chmod`/`chown`. You have to remount
the FS with the `metadata` option to enable it:

```sh
sudo umount /mnt/c
sudo mount -t drvfs C: /mnt/c -o metadata
```

There are also mount options for `uid`/`gid` mappings, and `umask`/`fmask` to
modify permissions. See the [blog
post](https://blogs.msdn.microsoft.com/commandline/2018/01/12/chmod-chown-wsl-improvements/)
for details.

### Launching Windows Applications

Since [build
14965](https://msdn.microsoft.com/en-us/commandline/wsl/release_notes#build-14965),
Windows applications can be easily launched from a WSL shell, as the NT user
path is by default appended to the Linux `$PATH`. Just try something like
`notepad.exe` or even go nuts and do `cmd.exe`.

The current (Linux) working directory is translated and passed to the Windows
application, as long as it is something below `/mnt/`; otherwise a warning will
be printed. So you can e.g. start VS Code in the current directory with `code .`

## Upgrade

Initial WSL (released with Win 10 Anniversary Update / v1607) shipped with Ubuntu
14.04 LTS (Trusty). With [WSL Build
14951](https://msdn.microsoft.com/en-us/commandline/wsl/release_notes#build-14951)
(which itself is available since Windows 10 Creators Update / v1703) Ubuntu
16.04 LTS (Xenial) is
[supported](https://blogs.msdn.microsoft.com/commandline/2016/10/19/wsl-adds-ubuntu-16-04-xenial-support/),
but not automatically upgraded.

To check versions:

* Windows: `winver.exe`
* WSL/Ubuntu: `lsb_release -a`

To upgrade an existing 14.04, you can either:

* uninstall/reinstall: `lxrun /uninstall /full /y` / `lxrun /install` (from
  `cmd` or PowerShell)
* upgrade in place: `sudo do-release-upgrade` (inside a running WSL shell)

The later seems to work fine, just like upgrading a "real" Ubuntu/Debian
installation. After the upgrade, a Windows reboot is needed.

## Backup / Restore

Installed WSL distros can be backed up to a tarball and later restored from that.  
This works for both WSL1 and WSL2 distros.

### Backup

```sh
wsl --export Ubuntu-18.04 Ubuntu-18.04.tar
wsl --export Ubuntu-20.04 Ubuntu-20.04.tar
```

### Restore

Target directory needs to exist. So in the example below, make sure to create
`C:\WSL\` first.

```sh
wsl --import Ubuntu-18.04 C:\WSL\Ubuntu-18.04 D:\WSL-backup\Ubuntu-18.04.tar
wsl --import Ubuntu-20.04 C:\WSL\Ubuntu-20.04 D:\WSL-backup\Ubuntu-20.04.tar
```

### Verification / Fixing Stuff

After the restore, the distro should be listed in `wsl --list -v`.  
You may want to change the default distro with `wsl --set-default`.

#### WSL Version

You probably have set WSL to default to v2, so both will be v2 distro.
If one of the distros is supposed to be v1, it can be downgraded like this:

```sh
wsl --set-version Ubuntu-18.04 1
```

#### Default User

Unfortunatelly, the default user is lost by the backup/restore (see
[this GitHub issue](https://github.com/microsoft/WSL/issues/3974)), so
launching the distro gives you a `root` shell.

The proper way to fix this would be:

```
<distro>.exe config --default-user <user> # <distro>.exe is e.g. ubuntu2004.exe
```

but the distro launcher (`ubuntu2004.exe`) is not part of the tarball, so
it's lost when moving the distro to a new Windows installation. Either make
a backup of the launcher as well, or you [wsldl](https://github.com/yuk7/wsldl)
as a replacement.

Without the original launcher or wsldl, this can also be fixed directly in
the registry (yes, the registry).

- get the UID of your WSL user: `id -u <user>` (it's probably `1000`)
- launch good ol' regedit, go to `Computer\HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Lxss`
- all distros are below that, check their `DistributionName` values to see which is which
- put the UID of your user into `DefaultUid` (make sure to enter as decimal, not hex)
- restart the distro (closing all instances should do it, or enfore with `wsl --terminate`)

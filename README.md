debian-on-termux
================

what is it
----------

- a shell script to install [Debian 9 (stretch)](https://www.debian.org/releases/stretch/) via [debootstrap](https://wiki.debian.org/Debootstrap) in a [Termux](https://wiki.termux.com/wiki/Main_Page) environment
- supported Debian versions include: stable (stretch), testing (buster), unstable
- supported architectures include: armel, armhf, arm64, i386, amd64

- if you have root there are additional features to extend it and install it on an external sd card. If these features are used without root if they don't fail they may be extremely unreliable or disfunctional.

how to use it
-------------

- install [Termux](https://termux.com/)
- download `debian_on_termux.sh` from [debian-on-termux](https://github.com/puzzlecube/debian-on-termux) into your termux home directory

        cd /data/data/com.termux/files/home
        apt update
        apt install git
        hash -r
- what? why would we use wget in termux? use git instead of #wget https://raw.githubusercontent.com/sp4rkie/debian-on-termux/master/debian_on_termux.sh

	git clone git://github.com/puzzlecube/debian-on-termux debian-on-termux

- STAY IN TERMUX HOME DIRECTORY
- note replace $SOME_CLI_EDITOR with whatever text editor you want from termux
	$SOME_CLI_EDITOR $* ~/debian-on-termux/debian-on-termux.sh

- make sure the file is executable by termux with chmod
	chmod 0777 ~/debian-on-termux/debian-on-termux.sh

- check the configuration lines near the top of the script for your target architecture, debian version and other preferences
- execute the script

        sh debian_on_termux.sh

- to watch the installation process type

        tail -F $your_configured_debian_root/debootstrap/debootstrap.log

- if all went well (takes about 30min on the hardware below) a script is created to enter the debian guest system

        enter_deb

        Usage: enter_deb [options] [command]
        enter_deb: enter the installed debian guest system

          -0 - mimic root (default)
          -n - prefer regular termux uid (termux-uid)
	  -u - emulate a linux user with a username and password

- sample usage: debian shell (stay in chrooted debian)
        
        bash-4.4$ enter_deb
        root@localhost:~#

- sample usage: debian one-shot command (execute in chrooted debian and return to the host environment)

        bash-4.4$ enter_deb -n id\; hostname\; pwd\; cat /etc/debian_\*
        uid=10228(u0_a228) gid=10228(u0_a228) groups=10228(u0_a228),3003,9997,50228
        localhost
        /home/u0_a228
        9.1
        bash-4.4$

- for suggestions or in the unlikely event of a problem just raise an issue [here](https://github.com/sp4rkie/debian-on-termux/issues/new):-)

alternatives
--------

- [Fedora](https://github.com/nmilosev/termux-fedora)
- [Arch](https://github.com/sdrausty/termux-archlinux)
- [Ubuntu](https://github.com/Neo-Oli/termux-ubuntu)
- [Origional Debian on termux](https://github.com/sp4rkie/debian-on-termux)
reference
---------

[How to install Debian 9.2 chroot termux? #1645](https://github.com/termux/termux-packages/issues/1645#issuecomment-337564650)
[Origional Debian on termux](https://github.com/sp4rkie/debian-on-termux)

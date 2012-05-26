Xenomai Lab
===========

A Platform for Digital Real-Time Control.

Installation
------------

A fairly standard procedure.

### Xenomai

Xenomai Lab needs Xenomai installed on the target system. Xenomai 2.5.5.2 and 
2.5.6 are known to be supported. To install Xenomai please refer to the [wiki](http://www.xenomai.org/index.php/Building_Debian_packages).

In addition to this, Xenomai Lab needs non-root real-time access. Instructions
for this are available [here](http://www.xenomai.org/index.php/Non-root_RT), but
an abridged tutorial for Ubuntu or other Debian based systems is available
in Appendix A.

### Dependencies

    $ sudo apt-get install libboost-graph-dev qt4-dev-tools build-essential

### Compile Xenomai Lab:

    $ qmake

    $ make

### Install

    $ sudo make install

### Uninstall

    $ sudo make uninstall

Appendix
--------

### Appendix A

Enabling non-root real-time access in Ubuntu (or other similiar Debian based
distros) consists in merely two steps. One must add the intended user to
the xenomai group, and then pass the xenomai group id to xenomai nucleus during
boot.

Adding a user to the xenomai group can be doing via usermod

    $ sudo usermod -a -G xenomai USERNAME

To confirm, we can check /etc/groups with

    $ cat /etc/group | grep xenomai

which would yield

    xenomai:x:123:USERNAME

This means the xenomai group id is **123**, and has for members only USERNAME.

To pass this argument to the nucleus is a question of adding the parameter to
grub. For example

    $ sudo gedit /etc/default/grub

And edit the line

    GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"

so that it has the argument at the end

    GRUB_CMDLINE_LINUX_DEFAULT="quiet splash xeno_nucleus.xenomai_gid=125"

Finally, updating grub will load the new configuration

    $ sudo update-grub

---
layout: post
title: "Installing The Unofficial Byobu in Archlinux"
date: 2011-10-06 00:20
comments: true
categories: 
- tips
- archlinux
---

If you love [byobu](https://launchpad.net/byobu), & u just decided
to join the [archers](http://www.archlinux.org), you probably will
miss it as you can't simply do `sudo pacman -S byobu`, since the
package isn't available on any of the offcial repositories.

DO NOT DESPAIR, there is an unofficial package at the
[aur](http://aur.archlinux.org/) (Arch User Repository). Just goto
[aur](http://aur.archlinux.org/) to search for it, & copy the link
to the tarball, then:

```
$ cd /tmp
$ wget http://aur.archlinux.org/packages/by/byobu/byobu.tar.gz
$ tar zxf byobu.tar.gz
$ cd byobu
$ makepkg
```

Depending on how mature ur system is, you may be prompted to
manually install some extra dependencies, note these & run:

```
$ sudo pacman -S <DEPENDENCIES>
```

With all dependencies installed, then:

```
$ makepkg
$ pacman -U *.xz
```

And you can start to rock-&-roll :)


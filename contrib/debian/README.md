
Debian
====================
This directory contains files used to package brofistd/brofist-qt
for Debian-based Linux systems. If you compile brofistd/brofist-qt yourself, there are some useful files here.

## brofist: URI support ##


brofist-qt.desktop  (Gnome / Open Desktop)
To install:

	sudo desktop-file-install brofist-qt.desktop
	sudo update-desktop-database

If you build yourself, you will either need to modify the paths in
the .desktop file or copy or symlink your brofist-qt binary to `/usr/bin`
and the `../../share/pixmaps/brofist128.png` to `/usr/share/pixmaps`

brofist-qt.protocol (KDE)


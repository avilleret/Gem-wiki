filmQT
===

movie loader using Apple’s QuickTime (OSX/W32)

# Description

Apple has never ported *QuickTime* to 64bit (starting with OSX-10.5).
Therefore, this plugin will only work in *32bit* mode.
Furthermore, starting with OSX-10.9, even the 32bit Frameworks have been removed.

The W32 version might still be available and usable though.

# Status

Only works on a limited (and diminishing) number of systems (W32, OSX<10.9, 32bit mode).

# Note 
On Windows 7, after installing Quicktime player, I have to add QTCF.dll beside `pd` binary to enable this plugin.
Maybe a reboot can fix this (and lots of other issues on Windows...) since QTCF.dll is already present in Quicktime folder.

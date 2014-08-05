How to build Gem on Mac OS X Mavericks 
======================================

This document describe how to build Gem on Mac OS X Maverick (OSX-10.9).

Requirements
------------

### Tool chain

#### Xcode command line tools

You need to download Xcode Command Line tools. It comes with Xcode but if you don't want to install full Xcode development package, you can run in a terminal: `xcode-select --install` and then click `Install` rather than `Get Xcode`.

#### brew

[brew](http://brew.sh) is a package manager for OSX that provides various libraries.
It is not strictly necessary to build Gem, but it comes in handy if you want to install third-party libraries.

#### pkg-config

`pkg-config` eases the use of various Development packages:
`brew install pkg-config`

#### gettext

You also need the GNU tool `gettext`.
You can install it from several package managers, but it doesn't seem to work with `brew` when I am writing this.
So I built it from sources.
Get the source here: [https://www.gnu.org/software/gettext/](https://www.gnu.org/software/gettext/)
And follow the README instruction to build it.

`gettext`is needed by automake tools. If it's not installed, it tries to make the job without it but in my case it failed, so I installed it.

Some people [reported](http://lists.puredata.info/pipermail/gem-dev/2014-08/006904.html) that they succeeded with *brew*'s `gettext` using the following command, but I haven't tried it (yet):

~~~~
$ brew install gettext
$ brew link gettext --force
~~~~


### pure-data

You need a recent version of `pure-data`.
The latest one can be found on [http://puredata.info/downloads](http://puredata.info/downloads)

Note that there are 32-bit and 64-bit version of pure-data.
But 64-bit Pd-extended is not well supported for now.
So maybe 32-bit is a good choice at first.

### get Gem's sources

~~~~
git clone https://github.com/umlaeute/Gem.git
~~~~

### third party libs
Gem has a plugin system which adds lot's of functionalities depending on installed libraries.
#### ImageMagick and FTGL
`brew install imagemagick ftgl` and this also install Freetype

#### Output
Mac OS X comes with an OpenGL framework but you can enable other outputs by adding some libraries:
`brew install sdl homebrew/versions/glfw2 homebrew/versions/glfw3`

Building process
----------------

### autogen.sh
If you clone the git repository, you have to build the building tool yourself from the root of the cloned directory:
`./autogen.sh`

### configure
Then configure the building chain with:

~~~~
./configure --enable-fat-binary=i386
~~~~

I use the `--enable-fat-binary=i386` to force 32bit binary because I'm building against Pd-extended 32bit.
If configure cannot find Pd (e.g. because you installed it in a non-standard location),
you have to tell it where to search by adding a flag like `--with-pd=/Applications/Pd-0.45-5.app/Contents/Resources/`.

You can configure to build against Pd-Vanilla/64bit with:

~~~~
./configure --with-pd=/Applications/Pd-0.45-4-64bit.app/Contents/Resources/
~~~~

Since this is should become a 64bit build, omit the `--enable-fat-binary` flag.

Then build with:

~~~~
make
~~~~



## enabling more plugins

Enabling plugins needs to happen right before *compiling* Gem (or the respective plugins).

### VLC - grab images using libVLC

Get [VLC](http://videolan.org) and install it (I assume it is installed into `/Applications/VLC.app`).

Unfortunately, VLC is not automatically detected, so you have to tell configure about it, by exporting the following environment-variables before running `./configure`:

~~~
export PKG_LIBVLC_CFLAGS="-I/Applications/VLC.app/Contents/MacOS/include"
export PKG_LIBVLC_LIBS="-L/Applications/VLC.app/Contents/MacOS/lib -lvlc"
~~~

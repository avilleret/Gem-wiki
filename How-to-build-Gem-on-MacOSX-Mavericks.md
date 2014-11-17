How to build Gem on Mac OS X Mavericks 
======================================

This document describes how to build Gem on Mac OS X Maverick (OSX-10.9).

Requirements
------------

### Tool chain

#### Xcode command line tools

You need to download the *Xcode Command Line tools*.
They come with Xcode but if you don't want to install full Xcode development package, you can run the following in a terminal

~~~~bash
$ xcode-select --install
~~~~

and then click `Install` rather than `Get Xcode`.

#### brew

[brew](http://brew.sh) is a package manager for OSX that provides various libraries.
It is not strictly necessary to build Gem, but it comes in handy if you want to install third-party libraries.

#### pkg-config

`pkg-config` eases the use of various Development packages:

~~~~bash
$ brew install pkg-config
~~~~

#### gettext

You also need the GNU tool `gettext`.
You can install it from several package managers, but it doesn't seem to work with `brew` when I am writing this.
So I built it from sources.
Get the source here: [https://www.gnu.org/software/gettext/](https://www.gnu.org/software/gettext/)
And follow the README instruction to build it.

`gettext`is needed by automake tools. If it's not installed, it tries to make the job without it but in my case it failed, so I installed it.

Some people [reported](http://lists.puredata.info/pipermail/gem-dev/2014-08/006904.html) that they succeeded with *brew*'s `gettext` using the following command, but I haven't tried it (yet):

~~~~bash
$ brew install gettext
$ brew link gettext --force
~~~~


### Pure Data

You need a recent version of `Pure Data` (Pd).
The latest one can be found on [http://puredata.info/downloads](http://puredata.info/downloads)

Note that there are 32-bit and 64-bit version of Pure Data.
But 64-bit Pd-extended is not well supported for now.
So maybe 32-bit is a good choice at first.

### get Gem's sources

~~~~bash
$ git clone https://github.com/umlaeute/Gem.git
~~~~

### third party libs
Gem has a plugin system which adds lot's of functionalities depending on installed libraries.

#### ImageMagick and FTGL
The following also installs dependencies (like Freetype):

~~~~bash
$ brew install imagemagick ftgl
~~~~

#### Output
Mac OS X comes with an OpenGL framework but you can enable other outputs by adding some libraries:

~~~~bash
$ brew install sdl homebrew/versions/glfw2 homebrew/versions/glfw3
~~~~

Building process
----------------

The following steps will build Gem from the commandline using `autotools`.
I assume that you have changed your working directory to the Gem root.

### autogen.sh
If you have cloned the git repository, you have to build the building tool yourself:

~~~~bash
$ ./autogen.sh
~~~~

### configure
Then configure the building chain with:

~~~~bash
$ ./configure --enable-fat-binary=i386
~~~~

I use the `--enable-fat-binary=i386` to force 32bit binary because I'm building against Pd-extended 32bit.
If configure cannot find Pd (e.g. because you installed it in a non-standard location),
you have to tell it where to search by adding a flag like `--with-pd=/Applications/Pd-0.45-5.app/Contents/Resources/`.

You can configure to build against Pd-Vanilla/64bit with:

~~~~bash
$ ./configure --with-pd=/Applications/Pd-0.45-4-64bit.app/Contents/Resources/
~~~~

Since this should become a 64bit build, omit the `--enable-fat-binary` flag.

#### Disabling specific frameworks

Apple has a rather aggressive strategy of deprecating and removing components from their system
(e.g. compared to how Microsoft deals with backward compatibility).

The *Carbon* framework has been deprecated in OSX-10.8.

The *QuickTime* framework has been deprecated in OSX-10.5 and is not available at all on 64bit platforms.
It has been replaced by the *QTKit* framework, which has been deprecated in OSX-10.7 in favour of the
*AV Foundation* framework.

While Gem tries to dynamically check whether a given framework is present/usable on your system,
it unfortunately does not a very good job.
Luckily you can help the build process, by manually disabling frameworks that you know are not useable
on your system (or that you don't want to use for some other reason)

When building for 64bit (or when using a newer OSX), you are strongly advised to disable both the
*QuickTime* and the *Carbon* framework, by passing the following flags to `configure`:

~~~~bash
   --without-QuickTime-framework --without-Carbon-framework
~~~~

### Build

Then build with:

~~~~bash
$ make
~~~~

## enabling more plugins

Enabling plugins needs to happen right before *compiling* Gem (or the respective plugins).

### VLC - grab images using libVLC

Get [VLC](http://videolan.org) and install it (I assume it is installed into `/Applications/VLC.app`).

Unfortunately, VLC is not automatically detected, so you have to tell `configure` about it, by adding the following flags when running `./configure`:

~~~bash
   --with-libvlc-CFLAGS="-I/Applications/VLC.app/Contents/MacOS/include" \
   --with-libvlc-LIBS="-L/Applications/VLC.app/Contents/MacOS/lib -lvlc"
~~~

After building, you have to symlink `libvlc` besides `gem_videoVLC.dylib` with : 

~~~~
mkdir lib
ln -s /Applications/VLC.app/Contents/MacOS/lib/libvlc.5.dylib lib/libvlc.5.dylib
~~~~

### GMERLIN - opening films
[gmerlin](http://gmerlin.sourceforge.net) is a generic media decoding library, that uses - among other libraries - [ffmpeg](http://ffmpeg.org).

Therefore install *ffmpeg* first (the additional arguments will install ALL optional dependencies for enhanced functionality):

~~~~bash
$ brew install ffmpeg $(brew info ffmpeg | egrep "^--with-")
~~~~

At time of writing, the last release of *gmerlin/gavl* has been a while ago, and is no longer compatible with recent *ffmpeg*.
Therefore you should get the latest development version via `svn`:

~~~~bash
$ svn checkout http://svn.code.sf.net/p/gmerlin/code/trunk/gavl
$ svn checkout http://svn.code.sf.net/p/gmerlin/code/trunk/gmerlin_avdecoder
~~~~

Then build the two libraries (first *gavl*, then *gmerlin_avdecoder* which depends on the former):

~~~~bash
$ cd gavl
$ ./autogen.sh
$ ./configure && make install

$ cd ..

$ cd gmerlin_avdecoder
$ ./autogen.sh
$ ./configure && make install
~~~~

At time of writing, I had to edit `gmerlin_avdecoder/po/Makefile.in.in` and change the value of `GETTEXT_MACRO_VERSION` at the beginning of the file to match the gettext-version installed on my system:

~~~~
GETTEXT_MACRO_VERSION = 0.19
~~~~

Once *gmerlin-avdecoder* is installed, running Gem's `./configure` will automatically detect and use this library.

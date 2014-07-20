How to build Gem on Mac OS X Mavericks 
======================================

This document describe how to build Gem on Mac OS X Maverick.

Requirements
------------

### Xcode command line tools

You need to download Xcode Command Line tools. It comes with Xcode but if you don't want to install full Xcode developpement package, you can run in a terminal : `xcode-select --install` and then click `Install` rather than `Get Xcode`.

### gettext

You also need the GNU tool `gettext`.
You can install it from several package managers, but it doesn't seem to work with `brew` when I am wrinting this.
So I built it from sources.
Get the source here : [https://www.gnu.org/software/gettext/](https://www.gnu.org/software/gettext/)
And follow the README instruction to build it.

`gettext`is needed by automake tools. If it's not installed, it tries to make the job without it but in my case it failed, so I installed it.

### pure-data

You need a recent version of `pure-data`.
The latest one can be found on [http://puredata.info/downloads](http://puredata.info/downloads)

Note that there are 32-bit and 64-bit version of pure-data.
But 64-bit Pd-extended is not well supported for now.
So maybe 32-bit is a good choice at first.

### get Gem's sources

`git clone git://git.code.sf.net/p/pd-gem/gem`

### third party libs
Gem has a plugin system wich adds lot's of functionalities depending on installed libraries.
#### ImageMagick and FTGL
`brew install imagemagick ftgl` and this also install Freetype

#### OpenGL
Mac OS X comes with GLU and OpenGL but it seems to be mandatory to install GLEW instead `./configure` fails :
`brew install glew`glut


Building process
----------------

### autogen.sh
If you clone the git repository, you have to build the building tool yourself from the root of the cloned directory :
`./autogen.sh`

### configure
Then configure the building chain with :
`./configure --without-libquicktime --without-ftgl --enable-multicontext --enable-fat-binary=i386`
I use the `--enable-fat-binary=i386` flag to force 32 bit binary.
The `--enable-multicontext` flag is experimental for now but needed to get a working `[gemwin]` pd-object.
`--without-libquicktime` disable legacy QuickTime support, it's time to switch to AV Foundation.



> Written with [StackEdit](https://stackedit.io/).
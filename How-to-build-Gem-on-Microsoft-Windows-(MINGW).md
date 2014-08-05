How to build Gem on Microsoft Windows using MinGW
=================================================


This document describes how to build Gem on W32 using [MinGW](http://www.mingw.org)


## Requirements

### Tool chain

#### MinGW

You need [MinGW](http://www.mingw.org) in order to install Gem.
Get the newest installer from their [website](http://www.mingw.org/wiki/Getting_Started),
and install (at least):

 - mingw-developer-toolkit
 - mingw32-base
 - mingw32-gcc-g++
 - msys-base

also make sure you have the following *dev* package installed

  - mingw32-pthreads-w32

I have used the default installation target, which will install everything to `C:\MinGW\`.
Since we need the *MinGW Shell* (which I find installed as `C:\MinGW\msys\1.0\msys.bat`),
I created a shortcut from my desktop to that batch-file.

MinGW automatically mounts the W32 drives. Therefore my Pd-installation is visible as

     /c/Programme/pd

I also like to have the Gem-sources available in my MinGW home-directory, so I added the
following line to the `C:\MinGW\msys\1.0\etc\fstab` file:

    C:/Users/zmoelnig/Development /home/zmoelnig/src

This tells MinGW to make the `Development` folder in my W32-home directory available
as the  `src` folder in my MinGW-home directory.

### Pure Data

You need the Pure Data sources to build Gem, either Pd-vanilla or Pd-Extended.
The easiest way is to download a zip for Windows from [http://puredata.info/downloads](http://puredata.info/downloads).
Then unpack it.

I installed Pd-vanilla and unzipped it into `C:\Programme\pd\`.
I will use this path in the rest of the tutorial.
Note that you probably should choose a path that **does not** contain spaces.
E.g. ~~`C:\Program Files\pd`~~ is bad, it's better to use `C:\pd`.

### Gem

Obviously you will need the Gem sources, to compile it.
See the [other WIKI pages](How-to-build-Gem-on-Microsoft-Windows) where to find it.

I put the sources into `C:\Users\zmoelnig\Development\GitHub\Gem`.

Now, whenever I open the *MinGW Shell*, I can do

~~~bash
cd ~/src/GitHub/Gem
~~~

to find my Gem-sources (see [above](#mingw), how mapped the W32 directories to MinGW paths).


### FTGL

For text rendering, the *FTGL* library is required.
If you don't need text display within Gem, you can skip this part, and add `--without-ftgl` to the *configure* flags.

Download [freetype](http://sourceforge.net/projects/freetype/) (2.5.3) and [FTGL](http://sourceforge.net/projects/ftgl) (2.1.3-rc5) and extract them (I extracted them to `C:\Users\zmoelnig\Development\3rdparty`, which is `~/src/3rdparty` on MinGW).

Then build them (in the *MinGW Shell*).

The *freetype2* build system will tell you (when running configure) that it detected "unix" as your system.
While this is not strictly true, just ignore it.

~~~bash
cd ~/src/3rdparty/freetype-2.5.3/
./configure
make install
~~~

After installing freetype2, we can build *FTGL*. 
We have to do a few hacks in order to make FTGL recognize the W32-names of the the OpenGL libraries (which are called `libopengl32` resp. `libglu32`, instead of the `libGL` and `libGLU` as found on un*x systems).

I hacked together a replacement for `m4/gl.m4`, which you can get [here](https://gist.github.com/umlaeute/044e2b501cd41198ecad). Get the file and copy it into `ftgl-2.1.3~rc5/m4/`, replacing the existing file.
Then run:

~~~bash
$ cd ~/src/3rdparty/ftgl-2.1.3~rc5/
$ ./autogen.sh
$ ./configure --with-gl-lib="-lglu32 -lopengl32"
$ make install
~~~

Since we will do *dynamic* linking, we need to put the dll's we just created into a place where W32 will find them.
A good start is, the directory where the Gem-binary will live (the root of the Gem sources):

~~~bash
$ cp /usr/local/bin/libfreetype*.dll ~/src/GitHub/Gem/
$ cp /usr/local/bin/libftgl*.dll     ~/src/GitHub/Gem/
~~~


## building

MinGW allows us to use the autotools.
So open up your MINGW-shell (see above) and run

~~~bash
$ cd ~/src/GitHub/Gem/
$ ./autogen.sh
$ ./configure                 \
   --with-pd=/c/programme/pd  \
   PKG_FTGL_CFLAGS="-I/usr/local/include $(freetype-config --cflags)"  \
   PKG_FTGL_LIBS="-L/usr/local/lib -lftgl"
~~~

The first option (`--with-pd=`) tells `configure` where to find Pd.

The `PKG_FTGL_...` variables tell the build-process how to find and use the font-rendering libraries.

~~~bash
$ make
~~~

If all went well, you should now have a `Gem.dll` in your directory, and hopefully a number of Gem-output externals and plugins:

~~~bash
$ ls *.dll
Gem.dll
gem_filmAVI.dll
gem_filmDS.dll
gem_imageSGI.dll
gem_videoDS.dll
gem_videoVFW.dll
gemw32window.dll
~~~

When trying to the so-created binary within Pd, you might get an error about missing dynamic libraries.

To solve this, locate the given library and copy it next to the `Gem.dll`.
Good starting places are `/mingw/bin` (aka `C:\MinGW\bin`) and `/usr/local/bin` (aka `C:\MinGW\msys\1.0\local\bin`).

Some libraries I needed to copy:

- libgcc_s_dw2-1.dll
- libstdc++-6.dll
- pthreadGC2.dll
- libfreetype-6.dll
- libftgl-2.dll

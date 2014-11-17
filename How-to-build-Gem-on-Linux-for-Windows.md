How to build Gem on Linux for Microsoft Windows using MinGW64
=============================================================


This document describes how to cross-compile Gem on Linux for W32 using [MinGW-W64](http://mingw-w64.sourceforge.net/)


## Requirements

### Tool chain

#### MinGW-W64

Install `MinGW-W64` for your distribution.

I'm using *Debian* (testing/unstable), so I can simply do:

    # aptitude install mingw-w64 mingw-w64-tools mingw-w64-i686-dev

This might also install a number of programs you don't need, including `FORTRAN` and `ADA` compilers.
You can uninstall them if you don't like them (or if you want to save a few MByte).

### Pure Data

You need the Pure Data sources to build Gem, either Pd-vanilla or Pd-Extended.
The easiest way is to download a zip for Windows from [http://puredata.info/downloads](http://puredata.info/downloads).
Then unpack it.

I installed Pd-vanilla and unzipped it into
    ~/lib/W32/
with `~` being my `${HOME}`-directory.
So the actual `pd.exe` can be found as `~/lib/W32/pd/bin/pd.exe`).
I will use this path in the rest of the tutorial.

#### runtime library
`msvcrt.dll` from Pd/bin/ conflicts with the one used by MinGW-W64.
For now i just disabled the one provided by Pd by renaming it to `.../pd/bin/msvcrt.dll_`

**LATER** check about the implications of this.
expected side-effects:
- Pd won't start without this dll.
- using MinGW-W64's `msvcrt.dll` might crash Pd.

In any case, if you want to use the `pd.exe` in this directory, you have to restore this library before running Pd.

In practice I haven't found this a problem, as
- when building, I use a local copy of Pd extracted to `~/lib/W32/pd/bin/pd.exe` on my linux partition.
- when running Pd/Gem, I use a Pd-installation in `C:\Program Files\pd\bin\pd.exe` on my W32 partition.

Since the two are not the same, disabling `msvcrt.dll` in the build-environment, does no harm to the runtime environment.

### Gem

Obviously you will need the Gem sources, to compile it.
See the [other WIKI pages](Getting-Sources) where to find it.

I put the sources into `~/src/puredata/externals/Gem`.


### third party libraries
Gem has a plugin system which adds lot's of functionalities depending on the installed libraries.
You will need to have these libraries installed when building Gem, in order to be able to use them.

Here we briefly discuss the use of some (optional) 3rd-party libraries that change the behaviour of the entire Gem system.
Also have a look at the [plugins](#plugins) section for adding even more functionality depending on 3rd-party libraries.




#### FTGL

For text rendering, the *FTGL* library is required.
If you don't need text display within Gem, you can skip this part, and add `--without-ftgl` to the *configure* flags.

Download [freetype](http://sourceforge.net/projects/freetype/) (2.5.3) and [FTGL](http://sourceforge.net/projects/ftgl) (2.1.3-rc5) and extract them (I extracted them to `~/lib/W32`).

Then build them.

The *freetype2* build system will tell you (when running configure) that it detected "unix" as your system.
While this is not strictly true, just ignore it.
I also disabled `png` support, as `./configure` wrongly detected my *linux* PNG-library.

~~~bash
$ cd ~/lib/W32/
$ ./configure --host=i686-w64-mingw32 \
        --prefix=${HOME}/lib/W32/usr  \
        --without-png
$ make install
~~~

After installing freetype2 (into some local directory within `~/lib/W32`), we can build *FTGL*. 
We have to do a few hacks in order to make FTGL recognize the W32-names of the the OpenGL libraries (which are called `libopengl32` resp. `libglu32`, instead of the `libGL` and `libGLU` as found on un*x systems).

I hacked together a replacement for `m4/gl.m4`, which you can get [here](https://gist.github.com/umlaeute/044e2b501cd41198ecad). Get the file and copy it into `ftgl-2.1.3~rc5/m4/`, replacing the existing file.
Then run:

~~~bash
$ cd ~/src/3rdparty/ftgl-2.1.3~rc5/
$ ./autogen.sh
$ ./configure --host=i686-w64-mingw32      \
        --prefix=${HOME}/lib/W32/usr       \
		--with-gl-lib="-lglu32 -lopengl32" \
		--with-ft-prefix=${HOME}/lib/W32/usr 
$ make install
~~~

Unfortunately `libfreetype2` (or is it `ftgl`??)
handles an our `--prefix` argument badly, so we need to fix some things.
In `${HOME}/lib/W32/usr/lib/libftgl.la`, you have to replace `/usr/local/lib/libfreetype.la` in the `dependency_libs` section with
`${HOME}/lib/W32/usr/lib/libfreetype.la` (replace `${HOME}` with your real home-directory).
E.g.

~~~bash
sed -e "s|/usr/local/lib/|${HOME}/lib/W32/usr/lib/|" \
    -i ${HOME}/lib/W32/usr/lib/libftgl.la
~~~
Since we will do *dynamic* linking, we also need to put the dll's we just created into a place where W32 will find them.
A good start is, the directory where the Gem-binary will live (the root of the Gem sources):

~~~bash
$ cp ~/lib/W32/usr/bin/libfreetype*.dll ~/src/puredata/externals/Gem/
$ cp ~/lib/W32/usr/bin/libftgl*.dll     ~/src/puredata/externals/Gem/
~~~

#### fribidi
In order to (properly) display text that does not have the default left-to-right flow
(e.g. Hebrew and/or Arabic texts), you need the GNU [FriBidi](http://www.fribidi.org) library.



## Building process

MinGW-W64 allows us to use the autotools.

For the following steps, I will assume that you have changed your working directory to the Gem root folder:

~~~bash
$ cd ~/src/puredata/externals/Gem/
~~~

### autogen.sh
If you have cloned the git repository,
you have to build the building tool yourself:

~~~bash
$ ./autogen.sh
~~~

### configure
Next we need to run `configure` in order to detect all installed libraries and setup the build chain:

~~~bash
$ ./configure                      \
      --host=i686-w64-mingw32      \
      --without-ALL                \
      --with-pd=${HOME}/lib/W32/pd \
	  --with-ftgl                  \
	  --with-ftgl-cflags="-I${HOME}/lib/W32/usr/include -I${HOME}/lib/W32/usr/include/freetype2" \
	  --with-ftgl-libs="-L${HOME}/lib/W32/usr/lib -lftgl"  \
      --with-vfw32
~~~

The `--host` option specifies the target architecture (i686-CPU (32bit!), Windows, using the mingw toolchain).
The `--with-pd` option tells `configure` where to find Pd (headers and libraries).
The `--without-ALL` option disables the use of all (optional) libraries (for now; when cross-compiling, some libraries get wrongly detected to be available).
The `--with-vfw32` option turns on video-capturing via the olde video-for-windows API.
The `--with-ftgl` options turn on font rendering support (according to how we compiled freetype2/ftgl; see above)


#### malloc
When cross-compiling, autotools assumes that `malloc` is not GNU-compatible,
and does some `#define` trickery, which fails badly on C++.
Luckily, there's a trick to force autotools into believing that malloc is fine.
Run this before running `./configure`:

    $ export ac_cv_func_malloc_0_nonnull=yes

### Build

Finally start the build by running:

~~~bash
$ make
~~~

This will take a while.

If all went well, you should now have a `Gem.dll` in your directory, and hopefully a number of Gem-output externals and plugins:

~~~bash
$ ls *.dll
Gem.dll
gem_filmAVI.dll
gem_filmDS.dll
gem_imageSGI.dll
gem_videoVFW.dll
gemw32window.dll
~~~

#### separate sources and build
If you want (like me) to use the same source-tree for multiple configurations (e.g. for building both a linux and a w32 version of Gem), you can easily do so by running  `configure` and `make` steps in a separate directory.

~~~bash
.../Gem$ mkdir build-w32
.../Gem$ cd build-w32
.../Gem/build-w32$ ./configure                        \
                         --host=i686-w64-mingw32      \
						 --without-ALL                \
						 --with-pd=${HOME}/lib/W32/pd \
						 --with-vfw32
.../Gem/build-w32$ make
~~~



#### Problems
At time of writing, the `modelOBJ` plugin is known to fail the build.
For now, you can ignore this.

In order to complete the built despite this error, use

~~~bash
make -k
~~~


### Try it

When trying out the so-created binary within Pd, you might get an error about missing dynamic libraries.

To solve this, locate the given library and copy it next to the `Gem.dll`.

Some libraries I needed to copy:

- `libgcc_s_sjlj-1.dll`
- `libstdc++-6.dll`
- `libfreetype-6.dll`
- `libftgl-2.dll`


<!---
- pthreadGC2.dll
-->

Good starting places (at least on Debian) are

- `/usr/lib/gcc/i686-w64-mingw32/4.9-win32/`
- `~/lib/W32/usr/bin/`


## plugins

**TODO**

### videoVLC

[VideoLAN's VLC](http://www.videolan.org/vlc/) comes with an SDK.
(Unfortunately it seems that only the `.exe` installer includes the SDK, not the `.zip` package).
Install `VLC` on your W32 partition, and copy the `sdk` folder (as found in `%ProgramFiles%/VideoLAN/VLC/sdk`)
as `${HOME}/lib/W32/VLC/sdk` to your linux partition.

When running Gem's `configure`, add something like the following to the configure-flags:

~~~bash
    $ ./configure \
       --with-libvlc \
       --with-libvlc-cflags="-I${HOME}/lib/W32/VLC/sdk/include" \
       --with-libvlc-libs="-L${HOME}/lib/W32/VLC/sdk/lib -lvlc" \
    #...
~~~

After compilation, copy the following files from `%ProgramFiles%/VideoLAN/VLC/` next to your `Gem.dll`:

- `libvlc.dll`
- `libvlccore.dll`


### QuickTime

As of 2015, the [QuickTime for Windows SDK](https://developer.apple.com/quicktime/) can still be downloaded from apple's website
(you need an *appleid* for that - iirc you need to be registered as a developer).

Install the SDK on your W32 partition, and copy it as `${HOME}/lib/W32/QuickTime` to your linux partition.

~~~bash
$ QT_CFLAGS="-I${HOME}/lib/W32/QuickTime/CIncludes"
$ QT_LFLAGS="-I${HOME}/lib/W32/QuickTime/Libraries -lQTMLClient"
$ for i in filmQT imageQT recordQT
do
 pushd plugins/${i}
 make \
    CPPFLAGS="${QT_CFLAGS}"                                                  \
	LIBS="${QT_LFLAGS} $(egrep '^LIBS = ' Makefile | sed -e 's|^LIBS = ||')" \
	pkglib_LTLIBRARIES=gem_${i}.la                                           \
	am_gem_${i}_la_rpath="-rpath '\$(pkglibdir)'"
 popd
done
$

~~~

You will *also* need to install [QuickTime for Windows](http://support.apple.com/kb/DL837) on the W32 machine, in order to use the plugins.

<!--- mingw cannot use ATL/MFC, so this is void (but hopefully will change)
### DirectShow

- Install [Windows Driver Kit Version 7.1.0.](http://www.microsoft.com/download/en/details.aspx?id=11800)
 - I only installed *Build Environments* (takes >1GB)

 - extract intersting parts
    `.../inc/atl71/`

- Install [DXSDK](http://stevenhickson-code.googlecode.com/svn/trunk/blepo/external/Microsoft/DirectX)

~~~bash
$ svn co http://stevenhickson-code.googlecode.com/svn/trunk/blepo/external/Microsoft/DirectX ~/share/WIN/SDK/DirectX
$ cd ~/share/WIN/SDK/DirectX
$ mv DXSDK/Include/vfwmsgs.h DXSDK/Include/VFWMSGS.H
~~~

-->

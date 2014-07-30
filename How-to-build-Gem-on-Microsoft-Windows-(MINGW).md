This document describes how to build Gem on W32 using [MinGW](http://www.mingw.org)


## Requirements

### Gem

Obviously you will need the Gem sources, to compile it.
See the [other WIKI pages](How-to-build-Gem-on-Microsoft-Windows) where to find it.

I put the sources into `C:\Users\zmoelnig\Development\GitHub\Gem`

### Pure data

You need the Pure data sources to build Gem, either the Vanilla or Extended version.
The easiest way is to download a zip for Windows from [http://puredata.info/downloads](http://puredata.info/downloads).
Then unpack it.

I unzipped it into `C:\Programme\pd\` and will use this path in the rest of the tutorial


### MinGW

You need [MinGW](http://www.mingw.org) in order to install Gem.
Get the newest installer from their [website](http://www.mingw.org/wiki/Getting_Started),
and install (at least):

 - mingw-developer-toolkit
 - mingw32-base
 - mingw32-gcc-g++
 - msys-base

also make sure you have the following **dev** package installed

  - mingw32-pthreads-w32

I have used the default installation target, which will install everything to `C:\MinGW\`.
Since we need the *MinGW Shell* (which I find installed as  `C:\MinGW\msys\1.0\msys.bat`),
I created a shortcut from my desktop to the batch-file.

MinGW automatically mounts the windows drives. Therefore my Pd-installation is visible as

     /c/Programme/pd

I also like to have the Gem-sources available in my MinGW home-directory, so I added the
following line to the `C:\MinGW\msys\1.0\etc\fstab` file:

    C:/Users/zmoelnig/Development /home/zmoelnig/src

This tells MinGW to make the `Development` folder in my W32-home directory available
as the  `src` folder in my MinGW-home directory.
Now, whenever I open the *MinGW Shell*, I can do

~~~bash
cd ~/src/GitHub/Gem
~~~
to find my Gem-sources
### FTGL

TO BE WRITTEN


## building

MinGW allows us to use the autotools.
So open up your MINGW-shell (see above) and run

~~~bash
$ cd ~/src/GitHub/Gem/
$ ./autogen.sh
$ ./configure --with-pd=/c/programme/pd
~~~

for whatever reasons this gave me an error
> GL (headers) not found! you need openGL!!!

which I ignored and proceeded

~~~bash
$ make
~~~
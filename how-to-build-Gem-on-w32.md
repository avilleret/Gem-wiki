How to build Gem in Microsoft Windows

## Preambule

This document was originally written with a French version of Visual C++ 2008 Express.
Menus and labels in this document might be translated from this version, and thus differ from the original ones.

## Requirements

### Visual C++

You need a Visual C++ environment to build Gem.
You can download and install Visual C++ 2010 Express.
A serial number is needed but you can get one for free from Microsoft.

NOTE: In Visual C++ you will find the *Properties manager* (*Gestionnaire de propriétés*) under the *View* (*Affichage*) menu.

If you have the Express edition, it is hidden...Click on *Tools -> Parameters -> Advanced parameters* (*Outils -> Paramètres -> Paramètres avancés*) to see it.

### Pure data

You need the Pure data sources to build Gem, either the Vanilla or Extended version.
The easiest way is to download a zip for Windows from [http://puredata.info/downloads](http://puredata.info/downloads).
Then unpack it.

### Pthread

Download the latest release from here:
[http://sourceforge.net/projects/pthreads4w/](http://sourceforge.net/projects/pthreads4w/)
and unpack it.

### FTGL and Freetype
You also need FTGL and Freetype libraries.

#### Freetype 
1. Unfortunately, Freetype 2.3.5 has some linking issues.
 So I used the latest version available 2.5.0, but there is no binary.
 Here is how to build it yourself. 
2. Download [freetype-2.5.0.tar.gz](http://download.savannah.gnu.org/releases/freetype/freetype-2.5.0.tar.gz) or something like that from [http://www.freetype.org/download.html](http://www.freetype.org/download.html).
3. Extract the zip file in a place you know and you may remember easily (e.g. I put it in : `C:\Users\win7\Bibliothèques\freetype-2.5.0\`)
4. Open the solution which fits best your environment (for Windows XP 32bit and Visual C++ 2010 Express it's `builds\win32\vc2010\freetype.sln`) 
5. Select the `Release Multithreaded` and `Win32` configurations then hit <kbd>F7</kbd>	to generate the solution. 
6. You should have a `freetype250MT.lib` under `objs\win32\vc2010` (or something else somewhere under the `objs` folder depending on your configuration). 
7. For the next steps, it is useful to setup a global environment variable called `FREETYPE` and pointing to the root of the freetype directory (where `objs` and `include` folders are). This is under the *advanced system properties* of Windows, its exact location depends on your Windows version. 

#### FTGL
1. Download FTGL from [http://sourceforge.net/projects/ftgl/](http://sourceforge.net/projects/ftgl/) 
2. Extract the tar.gz file (you may need a good archive extractor to do that, [7zip](http://www.7-zip.org/) is a good candidate) - again in a place you know and you may remember easily
3. Then open the `ftgl-2.1.3~rc5\msvc\vc8\ftgl_static.vcproj` file in Visual C++.
If you are not using VC8 the project should be converted automatically and please follow the wizard. You could also choose some project under other folder depending on your version.
4. Then generate the solution (you may need to save the solution first). And you will get a `ftgl_static.lib` file under the `msvc/build` folder. 

## Getting GEM sources

If you just want to build the last version of Gem but you do not planned to make modifications in the code, let's get a tarball from sourceforge or github of a fresh snapshot.

“Download a zip” here : [https://github.com/umlaeute/Gem](https://github.com/umlaeute/Gem)

or

“Download snapshot” here : [http://sourceforge.net/p/pd-gem/gem/ci/master/tree/](http://sourceforge.net/p/pd-gem/gem/ci/master/tree/)

If you plan to make some improvement on Gem (and I encourage you to do that) then it's better to clone the Git repository. But you need [git for windows](http://msysgit.github.io/)
to do that. Here I [quote IOhannes](http://lists.puredata.info/pipermail/gem-dev/2013-09/006564.html)  who explains his preferred way to contribute (and this is not Windows specific) :

> - go to [http://github.com/](http://github.com/) and get yourself an account (e.g. "rybn"),  then log in.  
> - go to [http://github.com/umlaeute/Gem](http://github.com/umlaeute/Gem), and click on the "Fork" button in the upper-right corner.  
> - this will fork the repository into [http://github.com/rybn/Gem](http://github.com/rybn/Gem), go  there and follow the instructions to clone the repository to your local machine.  
> - do work (add new abstractions/,...) and commit them to your local copy  
> - push them to github  
> - go back to [http://github.com/rybn/Gem](http://github.com/rybn/Gem) and click on "Pull Request" and follow the instructions there.  
> - I will get a notification that i should merge in your changes and can do so (after reviewing them) 

Then you have a folder containing all the sources files. Please read also `doc/CodingStyle.txt` before making changes.

## Configuring Gem solution in Visual C++

In the `Gem\build\win-vce2010`[4](#sdfootnote4sym) folder, you will find a `Gem.sln` file.
Some conversion may be needed if you are using another version of Visual C++.

Once the project imported, open the _Properties manager[5](#sdfootnote5sym)_ window and find the Puredata
configuration. Open it and adjust the PD_DIR macro under the _User macro_ page to point to your Pd folder.

In the *pthread properties sheet* change the PTHREAD_DIR and the PD_DIR macro to point to the `pthread` directory (for me it's `C:\Users\win7\Bibliothèques\pthreads-w32-2-9-1-release\Pre-built.2`)
and to the `pd` directory.

In the *FTGL properties sheet*, under the `FTGL Release` or the `FTGL Debug` configuration,
adjust the `FREETYPE` and the `FTGL` paths (e.g. `C:\Users\win7\Bibliothèques\freetype-2.3.5-1-lib` and `C:\Users\win7\Bibliothèques\ftgl-2.1.3~rc5`).

Now you will be able to generate at least the Gem project.

## Building plugins and addons

To build plug-ins, you will need several additional libraries.

### filmAVI – play films with Video for Windows

This plug-in should build without any additional library.

### filmDS – play films with Direct Show

You need the Microsoft Windows SDK : [http://msdn.microsoft.com/en-US/windows/desktop/bb980924](http://msdn.microsoft.com/en-US/windows/desktop/bb980924).
Some files lack in the one that comes with Visual C++ 2010 Express.

You need the Windows Driver Kit for ATL support : [http://msdn.microsoft.com/en-us/windows/hardware/hh852365](http://msdn.microsoft.com/en-us/windows/hardware/hh852365).
Get the one compatible with your IDE (7.1,0 for me)

Update the macros in the *DirectShow properties sheet*.

### filmQT – play films with QuickTime

You need the *QuickTime SDK for Windows*:
[https://developer.apple.com/quicktime/](https://developer.apple.com/quicktime/)
(you need an Apple Developper account to download it...).

If you install it in the default location ("`C:\Program Files`") you don't need to adjust any path.

### imageJPEG – load still image with libjpeg

You need libjpeg:
[http://gnuwin32.sourceforge.net/packages/jpeg.htm](http://gnuwin32.sourceforge.net/packages/jpeg.htm)

Download the _Developer files_ and extract it. Adjust the `LIBJPEG_DIR` macro in the *JPEG
properties sheet* to point where you extracted the files (e.g. `C:\Users\win7\Bibliothèques\jpeg-6b-4-lib`).

### imageTIFF – load still image with libtiff

You need the libtiff for Windows. Choose the _Developer files_
here: [http://gnuwin32.sourceforge.net/packages/tiff.htm](http://gnuwin32.sourceforge.net/packages/tiff.htm).
Then adjust the `LIBTIFF_DIR` macro in the *TIFF properties sheet*.

### pix_artoolkit – detect ARToolkit tag

You need the ARToolkit library for Windows:
[http://sourceforge.net/projects/artoolkit/files/artoolkit/](http://sourceforge.net/projects/artoolkit/files/artoolkit/).
The Windows binary release contains all what you need. Adjust the
`ARTOOLKIT_DIR` variable in *ARToolkit properties sheet*.

[4](#sdfootnote4anc)The
	**e** is for *E*xpress, not for *E*mbedded.

[5](#sdfootnote5anc)
	See FTGL and Freetype on page 1 if you can't find it.

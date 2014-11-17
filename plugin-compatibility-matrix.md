plugin compatibility matrix
====

this page contains a tabular list of the availability of plugins, depending on the various build systems.

# film plugins

| *plugin*                               | linux (Debian/64bit) | OSX (10.9/6bit) | W7 (32bit/MinGW) | W7 (32bit/MSVC)² |
| -------------------------------------- |:--------------------:|:---------------:|:----------------:|:----------------:|
|  [filmAVFoundation](filmAVFoundation)  | n/a                  | n/a             | n/a              | n/a              |
|  [filmAVI](filmAVI)                    | n/a                  | n/a             | ??               | build but can't play video ?|
|  [filmAVIPLAY](filmAVIPLAY)            | OK                   | ??              | ??               | ??               |
|  [filmDarwin](filmDarwin)              | n/a                  | **KO**          | n/a              | n/a              |
|  [filmDS](filmDS)                      | n/a                  | n/a             | ??               | OK               |
|  [filmGMERLIN](filmGMERLIN)            | OK                   | OK              | ??               | ??               |
|  [filmMPEG1](filmMPEG1)                | OK  (deprecated)     | ??              | ??               | ??               |
|  [filmMPEG3](filmMPEG3)                | OK                   | ??              | ??               | ??               |
|  [filmQT](filmQT)                      | n/a                  | **KO**          | ??               | OK               |
|  [filmQT4L](filmQT4L)                  | OK                   | n/a             | n/a              | n/a              |
|  [filmTEST](filmTEST)¹                 | OK                   | OK              | OK               | OK               |

# image plugins

| *plugin*                    | linux (Debian/64bit) | OSX (10.9/6bit) | W7 (32bit/MinGW) | W7 (32bit/MSVC)² |
| --------------------------- |:--------------------:|:---------------:|:----------------:|:----------------:|
|  [imageJPEG](imageJPEG)     | OK                   | OK              | ??               | ??               | 
|  [imageMAGICK](imageMAGICK) | OK                   | OK              | ??               | OK               |
|  [imageQT](imageQT)         | n/a                  | **KO**          | ??               | ??               |
|  [imageSGI](imageSGI)       | OK                   | OK              | OK               | ??               |
|  [imageTIFF](imageTIFF)     | OK                   | OK              | ??               | ??               |

# model plugins

note: currently all model-loading plugins are broken (at least for multicontext builds; see issue [#31](/umlaeute/Gem/issues/31)

| *plugin*                     | linux (Debian/64bit) | OSX (10.9/6bit) | W7 (32bit/MinGW) | W7 (32bit/MSVC)² |
| ---------------------------- |:--------------------:|:---------------:|:----------------:|:----------------:|
|  [modelOBJ](modelOBJ)        | OK                   | OK              | OK               | ??               |
|  [modelASSIMP2](modelASSIMP2)| OK                   | ??              | ??               | ??               |


# record plugins

| *plugin*                  | linux (Debian/64bit) | OSX (10.9/6bit) | W7 (32bit/MinGW) | W7 (32bit/MSVC)² |
| ------------------------- |:--------------------:|:---------------:|:----------------:|:----------------:|
|  [recordQT](recordQT)     | n/a                  | **KO**          | ??               | ??               |
|  [recordQT4L](recordQT4L) | OK                   | n/a             | n/a              | ??               |
|  [recordV4L](recordV4L)   | OK                   | n/a             | n/a              | ??               |
|  [recordV4L2](recordV4L2) | OK                   | n/a             | n/a              | ??               |

# video plugins

| *plugin*                         | linux (Debian/64bit) | OSX (10.9/6bit) | W7 (32bit/MinGW) | W7 (32bit/MSVC)² |
| -------------------------------- |:--------------------:|:---------------:|:----------------:|:----------------:|
|  [videoAVT](videoAVT)            | ?OK? (current??)     | n/a             | ??               | build and load but no device to test|
|  [videoDarwin](videoDarwin)      | n/a                  | ??              | n/a              | n/a              |
|  [videoDC1394](videoDC1394)      | OK                   | ??              | ??               | ??               |
|  [videoDS](videoDS)              | n/a                  | n/a             | ??               | rework in progress|
|  [videoDV4L](videoDV4L)          | OK                   | n/a             | n/a              | n/a              |
|  [videoHALCON](videoHALCON)      | ?OK? (current??)     | ??              | OK?              | build and load but no device to test|
|  [videoOptiTrack](videoOptiTrack)| n/a                  | ??              | OK               | build and load but no device to test|
|  [videoPYLON](videoPYLON)        | ?OK? (current??)     | n/a             | ??               | ??               |
|  [videoQTKit](videoQTKit)        | n/a                  | ??              | n/a              | n/a              |
|  [videoSGI](videoSGI)            | n/a                  | n/a             | ??               | ??               |
|  [videoTEST](videoTEST)¹         | OK                   | OK              | OK               | OK               |
|  [videoUNICAP](videoUNICAP)      | OK                   | ??              | ??               | not supported ?  |
|  [videoV4L](videoV4L)            | OK (deprecated)      | n/a             | n/a              | n/a              |
|  [videoV4L2](videoV4L2)          | OK                   | n/a             | n/a              | n/a              |
|  [videoVFW](videoVFW)            | n/a                  | n/a             | ??               | build and load but can't test|
|  [videoVLC](videoVLC)            | OK                   | OK              | OK               | crash at loading |



# notes

¹ *TEST* plugins are not built by default, though they work on all platforms.
they only generate test patterns, useful for - well - testing...
 
² build on W7 (32bit/MSVC) with Microsoft Visual C++ 2010 Express

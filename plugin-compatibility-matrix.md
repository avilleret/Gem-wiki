plugin compatibility matrix
====

this page contains a tabular list of the availability of plugins, depending on the various build systems.

# film plugins

| *plugin*                               | linux (Debian/64bit) | OSX (10.9/6bit) | W7 (32bit/MinGW) |
| -------------------------------------- |:--------------------:|:---------------:|:----------------:|
|  [filmAVFoundation](filmAVFoundation)  | n/a                  | n/a             | n/a              |
|  [filmAVI](filmAVI)                    | n/a                  | n/a             | ??               |
|  [filmAVIPLAY](filmAVIPLAY)            | OK                   | ??              | ??               |
|  [filmDarwin](filmDarwin)              | n/a                  | **KO**          | n/a              |
|  [filmDS](filmDS)                      | n/a                  | n/a             | ??               |
|  [filmGMERLIN](filmGMERLIN)            | OK                   | OK              | ??               |
|  [filmMPEG1](filmMPEG1)                | OK  (deprecated)     | ??              | ??               |
|  [filmMPEG3](filmMPEG3)                | OK                   | ??              | ??               |
|  [filmQT](filmQT)                      | n/a                  | **KO**          | ??               |
|  [filmQT4L](filmQT4L)                  | OK                   | n/a             | n/a              |
|  [filmTEST](filmTEST)¹                 | OK                   | OK              | OK               |

# image plugins

| *plugin*                    | linux (Debian/64bit) | OSX (10.9/6bit) | W7 (32bit/MinGW) |
| --------------------------- |:--------------------:|:---------------:|:----------------:|
|  [imageJPEG](imageJPEG)     | OK                   | OK              | ??               |
|  [imageMAGICK](imageMAGICK) | OK                   | OK              | ??               |
|  [imageQT](imageQT)         | n/a                  | **KO**          | ??               |
|  [imageSGI](imageSGI)       | OK                   | OK              | OK               |
|  [imageTIFF](imageTIFF)     | OK                   | OK              | ??               |

# model plugins

note: currently all model-loading plugins are broken (at least for multicontext builds; see issue [#31](/umlaeute/Gem/issues/31)

| *plugin*                     | linux (Debian/64bit) | OSX (10.9/6bit) | W7 (32bit/MinGW) |
| ---------------------------- |:--------------------:|:---------------:|:----------------:|
|  [modelOBJ](modelOBJ)        | OK                   | OK              | OK               |
|  [modelASSIMP2](modelASSIMP2)| OK                   | ??              | ??               |


# record plugins

| *plugin*                  | linux (Debian/64bit) | OSX (10.9/6bit) | W7 (32bit/MinGW) |
| ------------------------- |:--------------------:|:---------------:|:----------------:|
|  [recordQT](recordQT)     | n/a                  | **KO**          | ??               |
|  [recordQT4L](recordQT4L) | OK                   | n/a             | n/a              |
|  [recordV4L](recordV4L)   | OK                   | n/a             | n/a              |
|  [recordV4L2](recordV4L2) | OK                   | n/a             | n/a              |

# video plugins

| *plugin*                         | linux (Debian/64bit) | OSX (10.9/6bit) | W7 (32bit/MinGW) |
| -------------------------------- |:--------------------:|:---------------:|:----------------:|
|  [videoAVT](videoAVT)            | ?OK? (current??)     | n/a             | ??               |
|  [videoDarwin](videoDarwin)      | n/a                  | ??              | n/a              |
|  [videoDC1394](videoDC1394)      | OK                   | ??              | ??               |
|  [videoDS](videoDS)              | n/a                  | n/a             | ??               |
|  [videoDV4L](videoDV4L)          | OK                   | n/a             | n/a              |
|  [videoHALCON](videoHALCON)      | ?OK? (current??)     | ??              | OK?              |
|  [videoOptiTrack](videoOptiTrack)| n/a                  | ??              | OK               |
|  [videoPYLON](videoPYLON)        | ?OK? (current??)     | n/a             | ??               |
|  [videoQTKit](videoQTKit)        | n/a                  | ??              | n/a              |
|  [videoSGI](videoSGI)            | n/a                  | n/a             | ??               |
|  [videoTEST](videoTEST)¹         | OK                   | OK              | OK               |
|  [videoUNICAP](videoUNICAP)      | OK                   | ??              | ??               |
|  [videoV4L](videoV4L)            | OK (deprecated)      | n/a             | n/a              |
|  [videoV4L2](videoV4L2)          | OK                   | n/a             | n/a              |
|  [videoVFW](videoVFW)            | n/a                  | n/a             | ??               |
|  [videoVLC](videoVLC)            | OK                   | OK              | OK               |



# notes

¹ *TEST* plugins are not built by default, though they work on all platforms.
they only generate test patterns, useful for - well - testing...

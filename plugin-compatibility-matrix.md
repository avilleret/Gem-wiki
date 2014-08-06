plugin compatibility matrix
====

# film plugins

| *plugin*           | linux (Debian/64bit) | OSX (10.9/6bit) | W7 (32bit/MinGW) |
| ------------------ |:--------------------:|:---------------:|:----------------:|
|  filmAVFoundation  | ??                   | ??              | ??               |
|  filmAVI           | ??                   | ??              | ??               |
|  filmAVIPLAY       | ??                   | ??              | ??               |
|  filmDarwin        | ??                   | ??              | ??               |
|  filmDS            | ??                   | ??              | ??               |
|  filmGMERLIN       | ??                   | ??              | ??               |
|  filmMPEG1         | ??                   | ??              | ??               |
|  filmMPEG3         | ??                   | ??              | ??               |
|  filmQT            | ??                   | ??              | ??               |
|  filmQT4L          | ??                   | ??              | ??               |
|  filmTEST¹         | ??                   | ??              | ??               |

# image plugins

| *plugin*           | linux (Debian/64bit) | OSX (10.9/6bit) | W7 (32bit/MinGW) |
| ------------------ |:--------------------:|:---------------:|:----------------:|
|  imageJPEG         | ??                   | ??              | ??               |
|  imageMAGICK       | ??                   | ??              | ??               |
|  imageQT           | ??                   | ??              | ??               |
|  imageSGI          | ??                   | ??              | ??               |
|  imageTIFF         | ??                   | ??              | ??               |

# model plugins

note: currently all model-loading plugins are broken (at least for multicontext builds; see issue #31  )

| *plugin*           | linux (Debian/64bit) | OSX (10.9/6bit) | W7 (32bit/MinGW) |
| ------------------ |:--------------------:|:---------------:|:----------------:|
|  modelASSIMP2      | ??                   | ??              | ??               |
|  modelOBJ          | ??                   | ??              | ??               |

# record plugins

| *plugin*           | linux (Debian/64bit) | OSX (10.9/6bit) | W7 (32bit/MinGW) |
| ------------------ |:--------------------:|:---------------:|:----------------:|
|  recordQT          | ??                   | ??              | ??               |
|  recordQT4L        | ??                   | ??              | ??               |
|  recordV4L         | ??                   | ??              | ??               |
|  recordV4L2        | ??                   | ??              | ??               |

# video plugins

| *plugin*           | linux (Debian/64bit) | OSX (10.9/6bit) | W7 (32bit/MinGW) |
| ------------------ |:--------------------:|:---------------:|:----------------:|
|  videoAVT          | ??                   | ??              | ??               |
|  videoDarwin       | ??                   | ??              | ??               |
|  videoDC1394       | ??                   | ??              | ??               |
|  videoDS           | ??                   | ??              | ??               |
|  videoDV4L         | ??                   | ??              | ??               |
|  videoHALCON       | ??                   | ??              | ??               |
|  videoOptiTrack    | ??                   | ??              | ??               |
|  videoPYLON        | ??                   | ??              | ??               |
|  videoQTKit        | ??                   | ??              | ??               |
|  videoSGI          | ??                   | ??              | ??               |
|  videoTEST¹        | ??                   | ??              | ??               |
|  videoUNICAP       | ??                   | ??              | ??               |
|  videoV4L          | ??                   | ??              | ??               |
|  videoV4L2         | ??                   | ??              | ??               |
|  videoVFW          | ??                   | ??              | ??               |
|  videoVLC          | ??                   | ??              | ??               |



# notes

¹ *TEST* plugins are not built by default, though they work on all platforms.
they only generate test patterns, useful for - well - testing...
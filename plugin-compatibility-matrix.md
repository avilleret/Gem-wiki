plugin compatibility matrix
====

# film plugins

| *plugin*           | linux (Debian/64bit) | OSX (10.9/6bit) | W7 (32bit/MinGW) |
| ------------------ |:--------------------:|:---------------:|:----------------:|
|  filmAVFoundation  | n/a                  | n/a             | n/a              |
|  filmAVI           | ??                   | ??              | ??               |
|  filmAVIPLAY       | ??                   | ??              | ??               |
|  filmDarwin        | n/a                  | ??              | n/a              |
|  filmDS            | n/a                  | n/a             | ??               |
|  filmGMERLIN       | ??                   | ??              | ??               |
|  filmMPEG1         | ??                   | ??              | ??               |
|  filmMPEG3         | ??                   | ??              | ??               |
|  filmQT            | n/a                  | ??              | ??               |
|  filmQT4L          | ??                   | n/a             | n/a              |
|  filmTEST¹         | ??                   | ??              | ??               |

# image plugins

| *plugin*           | linux (Debian/64bit) | OSX (10.9/6bit) | W7 (32bit/MinGW) |
| ------------------ |:--------------------:|:---------------:|:----------------:|
|  imageJPEG         | ??                   | ??              | ??               |
|  imageMAGICK       | ??                   | ??              | ??               |
|  imageQT           | n/a                  | ??              | ??               |
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
|  recordQT          | n/a                  | ??              | ??               |
|  recordQT4L        | ??                   | n/a             | n/a              |
|  recordV4L         | ??                   | n/a             | n/a              |
|  recordV4L2        | ??                   | n/a             | n/a              |

# video plugins

| *plugin*           | linux (Debian/64bit) | OSX (10.9/6bit) | W7 (32bit/MinGW) |
| ------------------ |:--------------------:|:---------------:|:----------------:|
|  videoAVT          | ??                   | ??              | ??               |
|  videoDarwin       | n/a                  | ??              | n/a              |
|  videoDC1394       | ??                   | ??              | ??               |
|  videoDS           | n/a                  | n/a             | ??               |
|  videoDV4L         | ??                   | n/a             | n/a              |
|  videoHALCON       | ??                   | ??              | ??               |
|  videoOptiTrack    | ??                   | ??              | ??               |
|  videoPYLON        | ??                   | ??              | ??               |
|  videoQTKit        | n/a                  | ??              | n/a              |
|  videoSGI          | n/a                  | n/a             | ??               |
|  videoTEST¹        | ??                   | ??              | ??               |
|  videoUNICAP       | ??                   | ??              | ??               |
|  videoV4L          | ??                   | n/a             | n/a              |
|  videoV4L2         | ??                   | n/a             | n/a              |
|  videoVFW          | n/a                  | n/a             | ??               |
|  videoVLC          | ??                   | ??              | ??               |



# notes

¹ *TEST* plugins are not built by default, though they work on all platforms.
they only generate test patterns, useful for - well - testing...
plugin compatibility matrix
====

this page contains a tabular list of the availability of plugins, depending on the various build systems.

# film plugins

| *plugin*           | linux (Debian/64bit) | OSX (10.9/6bit) | W7 (32bit/MinGW) |
| ------------------ |:--------------------:|:---------------:|:----------------:|
|  filmAVFoundation  | n/a                  | n/a             | n/a              |
|  filmAVI           | n/a                  | n/a             | ??               |
|  filmAVIPLAY       | OK                   | ??              | ??               |
|  filmDarwin        | n/a                  | **KO**          | n/a              |
|  filmDS            | n/a                  | n/a             | ??               |
|  filmGMERLIN       | OK                   | OK              | ??               |
|  filmMPEG1         | OK  (deprecated)     | ??              | ??               |
|  filmMPEG3         | OK                   | ??              | ??               |
|  filmQT            | n/a                  | **KO**          | ??               |
|  filmQT4L          | OK                   | n/a             | n/a              |
|  filmTEST¹         | OK                   | OK              | OK               |

# image plugins

| *plugin*           | linux (Debian/64bit) | OSX (10.9/6bit) | W7 (32bit/MinGW) |
| ------------------ |:--------------------:|:---------------:|:----------------:|
|  imageJPEG         | OK                   | OK              | ??               |
|  imageMAGICK       | OK                   | OK              | ??               |
|  imageQT           | n/a                  | **KO**          | ??               |
|  imageSGI          | OK                   | OK              | OK               |
|  imageTIFF         | OK                   | OK              | ??               |

# model plugins

note: currently all model-loading plugins are broken (at least for multicontext builds; see issue [#31](/umlaeute/Gem/issues/31)

| *plugin*           | linux (Debian/64bit) | OSX (10.9/6bit) | W7 (32bit/MinGW) |
| ------------------ |:--------------------:|:---------------:|:----------------:|
|  modelOBJ          | OK                   | OK              | OK               |
|  modelASSIMP2      | OK                   | ??              | ??               |


# record plugins

| *plugin*           | linux (Debian/64bit) | OSX (10.9/6bit) | W7 (32bit/MinGW) |
| ------------------ |:--------------------:|:---------------:|:----------------:|
|  recordQT          | n/a                  | **KO**          | ??               |
|  recordQT4L        | OK                   | n/a             | n/a              |
|  recordV4L         | OK                   | n/a             | n/a              |
|  recordV4L2        | OK                   | n/a             | n/a              |

# video plugins

| *plugin*           | linux (Debian/64bit) | OSX (10.9/6bit) | W7 (32bit/MinGW) |
| ------------------ |:--------------------:|:---------------:|:----------------:|
|  videoAVT          | ?OK? (current??)     | n/a             | ??               |
|  videoDarwin       | n/a                  | ??              | n/a              |
|  videoDC1394       | OK                   | ??              | ??               |
|  videoDS           | n/a                  | n/a             | ??               |
|  videoDV4L         | OK                   | n/a             | n/a              |
|  videoHALCON       | ?OK? (current??)     | ??              | OK?              |
|  videoOptiTrack    | n/a                  | ??              | OK               |
|  videoPYLON        | ?OK? (current??)     | n/a             | ??               |
|  videoQTKit        | n/a                  | ??              | n/a              |
|  videoSGI          | n/a                  | n/a             | ??               |
|  videoTEST¹        | OK                   | OK              | OK               |
|  videoUNICAP       | OK                   | ??              | ??               |
|  videoV4L          | OK (deprecated)      | n/a             | n/a              |
|  videoV4L2         | OK                   | n/a             | n/a              |
|  videoVFW          | n/a                  | n/a             | ??               |
|  videoVLC          | OK                   | OK              | OK               |



# notes

¹ *TEST* plugins are not built by default, though they work on all platforms.
they only generate test patterns, useful for - well - testing...

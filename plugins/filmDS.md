filmDS
===

movie loader using DirectShow (W32)

On W7 (32bit/MSVC), [filmDS](filmDS) can load `alea.mpg` but I got some green flashes while playing.
It can also load and play `home.avi` without green flashes.
Loading `anim-1` failed with : `Unable to connect filters -2147220969`

Moreover after trying to load an unsupported video file, I can't open supported files anymore until restart Pd.

Also the image is vertically flipped.

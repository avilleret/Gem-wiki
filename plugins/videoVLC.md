videoVLC
===

video grabber using VLC

# Description


This plugin allows to open any media that VLC can read as if it was a live video
feed.



# building the plugin

#### autotools
If `./configure` does not automatically detect your installation of `libvlc`,
you can help it by passing the following flags (adjust paths to your system):
~~~bash
        --with-libvlc-CFLAGS="-I/c/Programme/VideoLAN/VLC/sdk/include" \
        --with-libvlc-LIBS="-L/c/Programme/VideoLAN/VLC/sdk/lib -lvlc"
~~~

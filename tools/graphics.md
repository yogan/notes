# Graphics

## Animated GIF

### Gifsicle

Command line tool for animated GIFs ([Gifsicle website](http://www.lcdf.org/gifsicle/)).

* installation: `apt install gifsicle`
* copypasta examples:
  * resize without smoothing (creating large pixels):
    `gifsicle --scale 5 < small.gif > large.gif`

### Converting videos to GIF with ffmpeg

Detailed article on how to produce
[high quality GIFs with ffmpeg](http://blog.pkh.me/p/21-high-quality-gif-with-ffmpeg.html).
TL;DR: use the proposed `gifenv.sh` (available in my `env/bin/`).

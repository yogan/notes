# Audio / Video

## Downsampling 7.1 AAC Audio Track to 5.1 AC3 (w/o Touching Video)

### Prelude: Completely Needless Rant about Media Players

All media players are pieces of shit. VLC freezes the video every time you take
a deep breath. Windows Media Player ("Movies and TV" or however they call this
garbage nowadays) cannot adapt audio streams to what the audio device can
actually play, and instead of giving any information about this, just goes the
passive aggresive way in punishes you with deadly silence.

Kodi is nice and all, but you don't want to boot up a full-blown media center
thingy all the time.

### Issue: Silence

Got some totally legal video with a fancy surround audio track, but can't hear
shit (see above). FFmpeg's `ffinfo` reveals the audio track is 7.1 AAC. That's
nice and all, but I only have a 5.1 setup from the middle ages, and (also see
above) Windows' "Movies and TV" thingy won't adapt that for me (VLC does, but 
freezes on every prime number video frame or so).

### Solution: Transcode the Audio

5.1 AC3 has worked for decades, so this should be good enough. FFmpeg can easily
do the audio conversion for me, without touching the video or subtitle tracks, so
it's also super fast:

```sh
ffmpeg -i legit_movie.mkv \
    -map 0 \                            # take all streams
    -vcodec copy -scodec copy \         # no touchy pls
    -acodec ac3 -b:a 640k \             # gimme sum audio I can hear, yo
    legit_movie_that_fucking_works.mkv
```


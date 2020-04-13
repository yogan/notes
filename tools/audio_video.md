# Audio / Video

## Downsampling 7.1 AAC Audio Track to 5.1 AC3 (w/o Touching Video)

### Prelude: Completely Needless Rant about Media Players

All media players are pieces of shit. VLC freezes the video every time you take
a deep breath. Windows Media Player ("Movies and TV" or however they call this
garbage nowadays) cannot adapt audio streams to what the audio device can
actually play, and instead of giving any information about this just goes the
passive aggressive way and punishes you with deadly silence.

Kodi is nice and all, but you don't want to boot up a full-blown media center
all the time.

### Issue: Silence

Got some totally legal video with a fancy surround audio track, but can't hear
shit (see above). FFmpeg's `ffprobe` reveals the audio track is 7.1 AAC. That's
nice and all, but I only have a 5.1 setup from the middle ages, and (also see
above) Windows' "Movies and TV" thingy won't adapt the audio for me (VLC does,
but freezes the video on every prime number video frame).

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

### Alternative: On the Fly Transcoding with mpv

As [suggested by @neverpanic](https://twitter.com/neverpanic/status/1249635747281473536),
[mpv](https://mpv.io) can do the conversion on the fly, while playing the video.
I always heard that mpv is pretty great, but I wasn't aware that it is
[available for Windows](https://mpv.io/installation) (there is even a
[chocolatey package](https://chocolatey.org/packages/mpv)), so I had not
considered it so far.

Turns out, it's pretty cool, and works just fine on Windows. After
[some struggles](https://twitter.com/yooogan/status/1249705703964577792)
with its [immense set of configuration options](https://mpv.io/manual/master/), I ended up
with this config snippet that does the job:

```config
# Let AC3 and DTS audio streams pass through to the A/V without touching.
# See: https://mpv.io/manual/master/#options-audio-spdif
audio-spdif=ac3,dts
#
# Here comes the magical part: *other* codecs (specifically DTS) get
# transcoded to AC3.
# See: https://mpv.io/manual/master/#audio-filters-lavcac3enc[
#
# scaletempo is needed to keep audio in sync when speeding up/down ([/]).
# Note that this does not work for audio streams directly passed through.
af=lavcac3enc,scaletempo
```

The options can either be passed directly when calling `mpv`
(`--audio-spdif=ac3,dts --af=lavcac3enc,scaletempo`), or added as shown above
to the config file (`~/.config/mpv/mpv.conf` on Lunix systems,
`%APPDATA%\mpv\mpv.conf` on Windows (symlinking works)).

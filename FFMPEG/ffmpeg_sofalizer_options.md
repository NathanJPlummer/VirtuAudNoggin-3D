___
##SOFALIZER OPTIONS (FFMPEG)
___
Consider the following command

"ffmpeg -i TestMySurround-en.dbr.ac3 -af -sofalizer sofa hrtf\ b_nh167.sofa -radius 3 -type time -o test.ac3"

I've used the following sofalizer options:

- radius (3)
- type (time)

Explanation of options and why I chose them:

- radius (3)

Radius is the amount of stereo expansion, measured in a dsitance of meters.  Set it too low and your surround effect will be compressed.  The distance between the "closest" and "furthest" sounds will be minimal and unnoticeable.

Set it too far and the effect becomes too pronounced.  Keep in my we want the listener to be able to maintain the illusion of a multispeaker system using headphones.  If the effect is "too good" we risk alerting the user we are using an algorithm.  This is both distracting to the user and ruins the allusion of surround.

- type (time)

This ones easier, according to the [FFMPEG manpage](https://ffmpeg.org/ffmpeg-filters.html#sofalizer) itself:

"Time is processing audio in time domain which is slow but gives high quality output. freq is processing audio in frequency domain which is fast but gives mediocre output. Default is freq."

Since we're using this as an encoder, where speed is less of an issue, and my goal for VirtuAudNoggin 3D is quality, we set this to "time."


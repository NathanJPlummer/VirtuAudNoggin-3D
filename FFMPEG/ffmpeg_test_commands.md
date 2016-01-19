___
###Update 1/18/2016 11:30PM
___

I managed to compile FFMPEG with options (bash script to be posted soon) and low and behold this worked!

**./ffmpeg -i testy.ac3 -af "sofalizer=~/SofaFF/hrtf_b_nh167.sofa" output.flac**

From there I needed to figure out the sytnax for the options I wanted to use.  After some trial and error, this got a great result.

**./ffmpeg -i testy.ac3 -af "sofalizer=~/SofaFF/hrtf_b_nh167.sofa:radius=3:type=time" output.flac**

I'll upload the bash script now.

___
###Update 1/18/2016 11 PM
___

According to [this](https://trac.ffmpeg.org/wiki/AudioChannelManipulation) website the synatax for solfalizer plugin is:

"ffmpeg -i input.wav -af sofalizer=/path/to/sofa/file output.flac"

Running this in Ubuntu- with both the system library and the static one provided by FFMPEG- still returns the "No such filter" error, which confirms my suspicion that I'll have to complie FFMPEG from source with the --enable-netcdf option to use sofalizer.  Working on a batch script to do this now.
___
###Original Post
___
Using the following test command in Ubuntu Wily:

**"ffmpeg -i TestMySurround-en.dbr.ac3 -af -sofalizer sofa hrtf\ b_nh167.sofa -radius 3 -type time -o test.ac3"**

- Documentation of why I chose these options located [here](https://github.com/NathanJPlummer/VirtuAudNoggin-3D/blob/master/FFMPEG/ffmpeg_sofalizer_options.md).

Results in the following error:

"ffmpeg version 2.7.3-0ubuntu0.15.10.1 Copyright (c) 2000-2015 the FFmpeg developers
  built with gcc 5.2.1 (Ubuntu 5.2.1-22ubuntu2) 20151010
  configuration: --prefix=/usr --extra-version=0ubuntu0.15.10.1 --build-suffix=-ffmpeg --toolchain=hardened --libdir=/usr/lib/x86_64-linux-gnu --incdir=/usr/include/x86_64-linux-gnu --enable-gpl --enable-shared --disable-stripping --enable-avresample --enable-avisynth --enable-frei0r --enable-gnutls --enable-ladspa --enable-libass --enable-libbluray --enable-libbs2b --enable-libcaca --enable-libcdio --enable-libflite --enable-libfontconfig --enable-libfreetype --enable-libfribidi --enable-libgme --enable-libgsm --enable-libmodplug --enable-libmp3lame --enable-libopenjpeg --enable-openal --enable-libopus --enable-libpulse --enable-librtmp --enable-libschroedinger --enable-libshine --enable-libspeex --enable-libtheora --enable-libtwolame --enable-libvorbis --enable-libvpx --enable-libwavpack --enable-libwebp --enable-libxvid --enable-libzvbi --enable-opengl --enable-x11grab --enable-libdc1394 --enable-libiec61883 --enable-libzmq --enable-libssh --enable-libsoxr --enable-libx264 --enable-libopencv --enable-libx265
  libavutil      54. 27.100 / 54. 27.100
  libavcodec     56. 41.100 / 56. 41.100
  libavformat    56. 36.100 / 56. 36.100
  libavdevice    56.  4.100 / 56.  4.100
  libavfilter     5. 16.101 /  5. 16.101
  libavresample   2.  1.  0 /  2.  1.  0
  libswscale      3.  1.101 /  3.  1.101
  libswresample   1.  2.100 /  1.  2.100
  libpostproc    53.  3.100 / 53.  3.100
Unrecognized option 'radius'.
Error splitting the argument list: Option not found"

At first I thought I was just passing options into FFMPEG wrong, so I tried this: (sofalizer filter, no additional options)

**"ffmpeg -i TestMySurround-en.dbr.ac3 -af -sofalizer test.ac3"**

Which resulted in THIS error:

"[AVFilterGraph @ 0x1a2fae0] **No such filter: '-sofalizer'**"

This means that either:
- My FFMPEG synatax is wrong
- Ubuntu's precompiled FFMPEG binary does not have sofalizer built in
- (Most likely) All of the above

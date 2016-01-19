___
#VirtuAudNoggin 3D ![Logo](http://i.imgur.com/aTQaCH6.png)
___
- Project to use Open Source tools to create a high quality HRTF encoding GUI
- [Logo License Information](https://github.com/NathanJPlummer/VirtuAudNoggin-3D/blob/master/Logo_License.md)

##Humble Start

If you're looking for some clever application or anything even remotely useful, move on.  This is nothing but a stream of conciousness concept right now.

I'm currently enrolled in a JavaScript programming class.  I'm a programming begginer.  This project is WAY out of my current abilities.  I'm sharing my ideas in case someone with better skills (pretty much anyone) has some insights, but for now, this is nothing more than a side project I can use to learn building applications.

FThere is currently no code here: for the time being this space will be used for nothing more than jotting down my thoughts and frustrations.

___
##What VirtuAudNoggin 3D is for
___

I have  an above average, 7.1 speaker system at home.  I'm a surround sound aficianado and will only buy the version of a film that has the highest quality soundtrack (right now this means Blu Ray).

If I'm on the go, OR it's late at night, I'm using headphones.  This could mean a labtop or my android phone.  What I'd like is to use an HRTF filter to create a "Virtual" sound environment.

While there are several solutions on the market for this, none provide a universal solution.  Current issues and implementations include:


##Operating Systems
- ###Android
	- The google play store has an [excellent soultion](http://www.iis.fraunhofer.de/en/pr/2013/20130725_GooglePlay.html)  from a company called Fraunhofer but it ONLY works on purchased movies from Google Play.  If you want to use it on your own movie files, you're out of luck.
	- With the exception of certain forms of AAC Android can not decode multichannel audio directly.  If you feed it a 5.1 or 7.1 source it will mix it to stereo.  An audio tool chain for a proper HRTF effect should be (example) 5.1 -> HRTF filter -> Stereo.  Since Android does the conversion automaticaly, your chain will be 5.1 -> Stereo -> HRTF.
	- The ONLY way around this is to encode your file with the proper toolchain BEFORE playing it back on Android.

- ###iOS
	- A few App that claims HRTF support via Dolby Headphone or "Out of Your Head" processesing.  Since I don't use OS X I have no idea how they work, or if iOS uses the proper audio toolchain for this.  It's possible they're just applying a spatialization filter to a stereo file.  Regardless, a preencode would make this unnecesary.

- ###OSX
	- Same as above.  There are a few realtime solutions, but no idea how or if they work.

- ###Linux
	- Has the best realtime solution, available [here](https://www.reddit.com/r/linux_gaming/comments/2ot5ov/enable_system_wide_hrtf_with_pulseaudio/).  However, method is not officially supported, documentation is poor, and different distributions use different commands to load the plugin, so this guide is unusable for many.
	- Has an encoder option but support is minimal and results are "clicky."  See "implementations" below.

- ###Windows
	- Most mainstream implementations supported but many are realtime only (not encoding, so can't create a file and then transfer to Android, for example).  Many have several caveats that make them less then optimal (see implementations). 

##Implementations

Below is a PARTIAL list only of the more common implementations of HRTF filters.

- ###Dolby Headphone
	- Generally favorable results
	- Realtime decoder only.  Encoding requires professional software not available to the public.
	- Stand alone hardware receivers use optical cables and can't process HD audio formats (DTS-HD, Dolby True-HD)
	- Software solutions are costly, built into video players, and can't be used outside intended software without complicated hacks.  So you can't use Dolby Headphone in, for example, a madVR MPC-HC configuration.
	- No Linux or Android applications

- ###DTS Headphone: X 11.1
	- Early reactions have been very impressive
	- Realtime only
	- Very limited market.  Only available on a select few devices
	- No software version at this time, so has all the same caveats at Dolby Headphone.

- Creative SBX Pro Studio
	- Mixed reviews.  Better for gaming.
	- Mostly hardware.  Software solution hasn't been updated in years.
	- Requires user to set up audio toolchain his/herself.  Complicated for movies.

- Razer Surround
	- Generally considered comparable in quality to Dolby Headphone
	- But can only process audio in 16-bits
	- Software only
	- No encode option
	- Windows only

- MIT HRTF
	- Generally considered low quality ("clicky" sounds)
	- But can be used in realtime or as an encoder
	- via Mplayer2/MEncoder2 or MPV
	- MPV support may be borked and requires complicated setup by user

- VLC
	- Software video player with HRTF filter
	- Not updated.  Lead audio developer left project...
	- ...and was [not an audio engineer](https://github.com/mpv-player/mpv/issues/1073).
	- So generally not great, and not included in Android port for practical reasons.
	
##Sofalizer

Sofalizer is a software filter designed to be a [high quality replacement](http://comments.gmane.org/gmane.comp.video.videolan.vlc.devel/99446) to the VLC spatializer.  Currently it has not been accepted into VLC though a port has been implented into the [FFMPEG source code](https://ffmpeg.org/ffmpeg-filters.html#sofalizer).

Sofalizer works by loading one of many available "sofa" filters.

Due to its open-source nature, and its inclusion intoo FFMPEG, it theoretically has the following advantages.

- Available for all operating systems with proper tool chain support (Windows, OSX, Linux, *ios???*).
- Availabe as an encoder (via ffpmeg)
- Available as a realtime decoder
	- Hopefully via VLC eventually
	- And probably now via FFPlay (not tested)

##Current Issues
- [Requires special compiling rules](https://www.mail-archive.com/ffmpeg-cvslog@ffmpeg.org/msg17711.html) and hence likely not available for most pre-compliled FFMPEG binarys.
- No Gui tools for use
- [Poor FFMPEG documentation](https://ffmpeg.org/ffmpeg-filters.html#sofalizer)
	- Though this could be due to my lack of skills properly using FFMPEG
- Limited documentation of [differences](http://www.sofaconventions.org/mediawiki/index.php/Files) in [external SOFA files](http://sofacoustics.org/data/database/ari%20(altb)/).
	- Again, this may be a knowledge gap on my part.

##Workflow and Version Goals of VirtuAudNoggin

###Workflow
1.  Decipher FFMPEG commands to filter audio with sofalizer
2.  If necesarry, compile proper version of FFMPEG
3.  Create GTK Gui using glade

###Version Goals for VirtuAudNoggin 3D
v1.  Encoder- Spatialize multichannel audio while "passthrough" video (no video reencode).  Find best "generic" .sofa file. Simple one option gui.

V2.  Decoder/Realtime option-  Allow user to load file and play through FFPLAY

v3.  Add option for user to choose/load choice of sofa filter.

v4.  Add option to choose output audio codec (MP3, AAC, FLAC, etc).

v5.  Port to Windows

v6.  Simple video reencode options (most common) to conserve filespace

v7.  Port for OSX.

	
	

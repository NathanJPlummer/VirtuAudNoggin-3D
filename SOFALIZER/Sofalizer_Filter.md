___
###Choosing a sofalizer filter
___

Sofalizer requires an external filter to create an HRTF output.  The [directory](http://sofacoustics.org/data/database/ari%20(altb)/) lists several and only [some documentation](http://www.sofaconventions.org/mediawiki/index.php/Files) is provided.  Since I'm trying to start with the best "general purpose" filter, my choice was based on a combination of the documentation as well as some admittedly pretty far out assumptions.

Let's start with what we do know:

From the [documentation](http://www.sofaconventions.org/mediawiki/index.php/Files)- bold emphasis added by me.

- ARI: HRTFs from the ARI database. In-the-ear HRTFs and DTFs for over 100 listeners.
	- hrtf, dtf: HRTFs and DTFs, respectively, equalized between 300 Hz and 18 kHz
	- **hrtf b, dtf b: HRTFs and DTFs, equalized between 50 Hz and 18 kHz for hi-fi auralizations**
- **ARI (ALTB): HRTFs from the ARI database. Measurements for some of the listeners from the ARI database, repeated and evaluated a few years later, see Majdak et al. (2013).**
- CIPIC: HRTFs from the CIPIC database. 45 listeners, partially antropometric data available.
- RIEC: Far-field HRTFs from the RIEC database of over 100 human listeners. (Credit: Kajni Watanabe, Japan)

This helps a bit, but the documentation is not consumer friendly.  I don't know what most of these terms mean, and perhaps someone could enlighten me.  For now, here's the first round of assumptions I made.

- More listeners = Increased result quality
- The "b" patterns have a larger dynamic range, and will be better suited for high bitrate content (DTS-HD, Dolby True HD)
- Newer measurements = More data, better accuracy.

For these reasons, I focused on [ARI (ALTB)](http://sofacoustics.org/data/database/ari%20(altb)/).

If you click that link you'll see a whole bunch of files and numbers, with little mention of what the numbers mean.  I know I'm looking for an HRTF b filter, but beyond that, the choices aren't obvious.  Again I'm going to make an assumption.

- The number is assigned to the listener

The description for the database says they used "Over 100 samples" and the file numbers go up to 167, so it's possible.

If that's the case though, this really is no help.  If they provided some characteristics about the listeners, say, head size, I could try to calculate some sort of statistical average and pick a "best general filter" from there.  Sadly, that data is not provided.

So from here, my assumptions get even wilder:

- The largest number = the last experiment = the experimenter had the most experience with equipment = less likelihood of human error.

That's a pretty statistically weak connection, all things considered.  I used to study psychology, and I can tell you something as simple of "How long ago did the experimenter have lunch?" would be a better way of accounting for possible human error.

That being said, I can only work with the dataset provided, so for the first test filter I'm choosing:

[hrtf b_nnh167.sofa](http://sofacoustics.org/data/database/ari%20(altb)/hrtf%20b_nh167.sofa)

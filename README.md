# Ted_labview_YouTube
Theodore's Labview Repository for YouTube (public)


Some instructions:


<h1> Install notes: </h1>
When installing labview, I used Linux Mint 20 (Ulyana) to install.
Labview only supports RedHat, OpenSUSE and scientific Linux. However, i was able to get it done on Linux Mint 20, an Ubuntu based distro.

I used a student edition, so install instructions may differ for different campuses or license holders.

https://forums.ni.com/t5/LabVIEW/Can-i-install-labVIEW-on-Ubuntu/td-p/3588236?profile.language=en

The idea for the linux iso is to navigate to the iso directory and run:

sudo sh ./INSTALL

this will install labview into 

/usr/local/natinst

For Linux Mint Debian Edition 4 (LMDE 4, Debbie), i have not been able to get it to install or run right as of 21 sep 2020.
Not going to try for sake of time

This was the closest guide for installing labview on Debian 10 buster, which should work on LMDE 4 as well since it's based on Debian.
https://www.martinholub.com/code/2019/04/28/InsatllingLabVIEW.html


<h1> Example 1 (wav_reader.vi)  notes: </h1>

In Example 1, i attempt to connect the microphone to labview in linux (Linux mint ulyana) and i find that some of these videos are helpful:

https://www.youtube.com/watch?v=Q7UJ_uOvXP8

And according to the national instruments (NI) website, linux requires Open Sound System (OSS) drivers to work:

http://zone.ni.com/reference/en-XX/help/371361R-01/lvconcepts/soundvis/

Here's OSS for Debian:

https://wiki.debian.org/OSS/


And for Ubuntu:
https://help.ubuntu.com/community/OpenSound

Note that OSS is currently freeware, it was commercial for awhile but you can find source code online.

https://en.wikipedia.org/wiki/Open_Sound_System

Anyhow you need it for sound vis to work...

Sound vis are a good starting point for frequency domain stuff to happen.

However, OSS on linux mint 20 is more than a pain (I can't get it to work without messing around with my system sound), and indeed i have no sound after installing OSS.

<h2> working with wav files </h2>

The alternative is to record a wav file using audacity.

And then importing the wav files into audacity.

This video is helpful


So the first example was to produce time domain chart from a waveform, ie audio file.


<h1> fast fourier transform </h1>

Now we want to start working with frequencies as well.

So we first want to try working with fast fourier transform (FFT).

It will plot an array of amplitude vs frequency bin (not absolute frequency).

Note that FFT will have this mirror effect so that the left half of the graph is a mirror of the right

A good explanation of such vis can be found here:

https://zone.ni.com/reference/en-XX/help/371361R-01/lvanls/fft/




<h1> power spectrum </h1>

if you want a quick way to see the frequency spectrum, then the best way is to use spectral measurements using the express vi.

It will be able to give you the exact frequencies that you will be noting.

I have a sound file which is a C in the guitar string going at 130 Hz.

You can use it to test things out...


<h1> FFT part ii </h1>

Well, you know, fast fourier transform doesn't quite give a plot of amplitude vs frequency.

So graph's rather hard to read.

How then do you read it?

One clue:

Set the number of elements to 44100 in FFT, that is FFT length is 44100.

Notice how the C3 note now has a peak at frequency bin 130ish, 264 and 396.

Why so special?

Note that the sampling frequency of the wav file is 44100, try doing it in audacity. I can do another note (G or A).


So G or A, They have a slightly different frequency. But the sampling frequency for audio files is still 44100 Hz or 44.1 kHz. 48 kHz is for ultra high def audio.


What is sampling frequency anyway?

https://www.izotope.com/en/learn/digital-audio-basics-sample-rate-and-bit-depth.html

This above website will help in understanding.


How does this relate to the frequency bins?


well, do take a look at the labview FFT vi help.


You will see how the FFT works.


one good video for you is this one by Steve Brunton.

https://www.youtube.com/watch?v=E8HeD-MUrjY


you can see that in the labview help,
the increment in frequency between each frequency bin is sampling frequency / no. of samples.


So for audio files, 44100 samples are taken each second, and we have 280,000 ish samples. So this is about 6s of data...


What is the change in frequency?

44100/280000 for my C note file. or about 1/6. Also note that this is 1/time where time is the time of the audio file.


Now that we know this, how do we put all this into labview?

We'll need to learn how to deal with arrays.

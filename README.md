# podcast-scripts
NPSCast Podcast Production Scripts

Feel free to branch, fork, use, or modify these as you see fit. These are written for my workflow, so modify the scripts to meet your needs. Some sections on the publish script are commented out, these are ones I don't use any more. Uncomment them if you want to use them. For the sections I use they aren't commented out, so feel free to comment them out if you don't need them.

### What do they do?

publish - Grab the .wav file and make a MP3 file while truncating the silence to no more than 1.0 seconds. Then it grabs your thumbnail image and adds your episode number to it, creates on the tags for the MP3 file, finishes up the show notes, uploads the HTML file for the show notes to the web server, runs WP-CLI to create the Wordpress Post, and it generates transcripts using Whisper-cpp

encode - Just encodes a wav file to mp3 while adding the ID3 tags without the artwork.

split -  Splits the multitrack wav files recorded by the Tascam MixCast 4 into mono tracks for the mics, and stereo for everything else, then merges the files if the original had been split. For example, if the MixCast splits the recording into two files, then microphone 1 will be split out from both recordings, then merged together into one file, as will happen for the other channels. If it's stereo at the fader, i.e. USB, the USB file will be stereo.

### Usage

publish does not accept command line arguments, it gather data from questions.

Encode can accept one file name like:

encode file.wav

mixcast-split can accept two file names like:

mixcast-split file1.wav file2.wav  

split-st is for stereo files and accepts one file name

split-st file1.wav

### Dependences

- FFMPEG
- ImageMagick
- rsync
- discount
- wpcli
- sox
- Whisper-cpp

Of course if you remove some of the features, then some of these dependencies would be removed.

### Setup

Update the configuration section at the top of each script.

### To Do

- shownotes still has some details that are too specific to my setup and I need to move them to the config.
- publish needs more of the features to be able to be turned off.

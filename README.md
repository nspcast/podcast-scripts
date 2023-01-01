# podcast-scripts
NPSCast Podcast Production Scripts

Feel free to branch, fork, use, or modify these as you see fit. These are written for my workflow, so modify the scripts to meet your needs. 

### What do they do?

publish - Grab the .wav file and make a MP3 file while truncating the silence to no more than 1.0 seconds. Then it grabs your thumbnail image and adds your episode number to it, creates on the tags for the MP3 file, finishes up the show notes, uploads the MP3 and artwork to s3 compatable object storage, uploads the HTML file for the show notes to the web server, runs WP-CLI to create the Wordpress Post, and it can encode a video for you as well.

shownotes - Grab stub files from your note taking solutions and automation data gathering to compile the episodes show notes. Also download voicemail from Twilio if you use that.

encode - Just encodes a wav file to mp3 while adding the ID3 tags without the artwork.

split -  Splits the multitrack wav files recorded by the Tascam MixCast 4 into mono tracks for the mics, and stereo for everything else, then merges the files if the original had been split. For example, if the MixCast splits the recording into two files, then microphone 1 will be split out from both recordings, then merged together into one file, as will happen for the other channels. If it's stereo at the fader, i.e. USB, the USB file will be stereo.

### Usage

publish and shownotes do not accept command line arguments, they gather data from questions.

Encode can accept one file name like:

encode file.wav

Split can accept two file names like:

split file1.wav file2.wav  

### Dependences

- FFMPEG
- ImageMagick
- rsync
- s3cmd
- discount
- wpcli
- sox
- Whisper

Of course if you remove some of the features, then some of these dependencies would be removed.

### Setup

If you only have one show, then update default.conf to match your show's details.
If you have more than one show, then make a copy of default.conf for each of your shows using the show's short prefix as the name, such as ab.conf and cd.conf. Be sure that you remove default.conf before you run the install script.

If you're going to use Twilio for voicemail, the populate the twilio.conf file.

If you run ./install it will copy the scripts to /usr/local/bin/ and .conf files to ~/.config/nspcast/
The install script will also handle updates, but will not copy anything to ~/.config/nspcast if that directory exists, so it won't overwrite your configurations.

### To Do

- shownotes still has some details that are too specific to my setup and I need to move them to the config.
- publish needs more of the features to be able to be turned off.

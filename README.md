
This is a helper script to simplify converting my MakeMKV rips for Chromecast and similarly constrained devices. It is made to be as pain free as I can make it for that purpose. Not a Swiss Army Knife, for that you just have to RTFM about ffmpeg.


    usage: ./pyffconv [-h] [--debug] [-F FORMAT] [-f FORMAT] [-i] [-r]
                      [-d STREAM_NUMBER] [-c STREAM_NUMBER]
                      ...

    Convertion tool built in Python and using ffmpeg.

    positional arguments:
      file_list

    optional arguments:
      -h, --help            show this help message and exit
      --debug               For developers.
      -F FORMAT, --output-format FORMAT
                            Force output container to be in FORMAT.
      -f FORMAT, --input-format FORMAT
                            Force input container to be detected as FORMAT.
      -i, --information     Verbose dump of file contents.
      -r, --report          Concise report of file contents.
      -d STREAM_NUMBER, --downmix STREAM_NUMBER
                            Create stereo downmix and surround from surround
                            STREAM_NUMBER.
      -c STREAM_NUMBER, --commentary STREAM_NUMBER
                            Mark STREAM_NUMBER as commentary.

Here's an example:

    $ ./pyffconv --downmix 1 --commentary 2 movie.mkv chromy.mp4

If the input was like this:

    stream 0: video
    stream 1: surround sound
    stream 2: commentary sound

Output will be like this:

    stream 0: video
    stream 1: downmixed sound
    stream 2: surround sound
    stream 3: commentary sound

*Note* that --commentary is still a work in progress and may eat babies.


ASSUMPTIONS
-------------

0. You have a suitable version of Python.
1. You have a suitable version of ffmpeg.
2. Your output format is likely mp4.

In the case of Python, I used Python 2.7.3 on Debian 7. Others should work but are not tested. See REQUESTS.

In the case of ffmpeg, I used version 2.1.1 built from source. Any issues with format support may be due to your ffmpeg build. I do not use or test with avconv or its ffmpeg wrapper.


Inputs / outputs I typically use are matroska and mp4 respectively. YMMV with other crap.


REQUESTS
========

- Issue reports should be filed at GitHub.
- Patches are likely welcome unless they do undesired things.

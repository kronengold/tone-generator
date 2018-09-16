# tone-generator
A Python script to create audio files based on frequecny, frame rates and length.
The script was tested with Python 3.6.

The arguments can be given by command line arguments or by using a GUI, which is based on PySimpleGUI.

The scripts can use command line arguments:
For example:
  tonegen -f 440 -r 44100 -t 5 -g
  where:
    f: frequeny in Hz
    r: frame rate in frames/second
    t: length of audio file in seconds
    g: Graphics Userr Interface (GUI)

if the '-g' argument is provided, a dialog box appears with any of the typed in arguments (not all have to be provided). If '-g' is not provided, all of the arguments must be provided.

The result is a WAV file, named as follows:
For example:
  440Hz_2.0s.wav
  Where the name parts are:
    440Hz_- the provided frequency, in Hz, followed by an underscore
    2.0s - audio lenght, in seconds
    .wav - the extension of the audio format

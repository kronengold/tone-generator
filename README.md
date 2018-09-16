# tone-generator
A Python script to create audio files based on frequecny, frame rates and length.
The script was tested with Python 3.6.

The script takes 3 arguments: frequency, frame rate and duration to generate a pure tone audio file in WAV format.

In case an ultrasonic tone is required, an adequate, higher frame rate is required to sample it correctly.

## Usage
The arguments can be given by command line arguments or by using a GUI, which is based on PySimpleGUI.

The scripts can use command line arguments:

    For example:

        *python tonegen.py -f 440 -r 44100 -t 5 -g*
  
        where:
  
            f: frequeny in Hz
    
            r: frame rate in frames/second
    
            t: length of audio file in seconds
    
            g: Graphics Userr Interface (GUI)
    
    
if the '-g' argument is provided, a dialog box appears with any of the provided arguments (none of the arguments is mandatory). If '-g' is not provided, all of the arguments must be provided.

## Output File
The result is a WAV file, named as follows:

    [Frequency]Hz_[time]s.wav
 
For example:

    440Hz_2.0s.wav
  
      Where the name is composed of:
  
          440Hz_- the provided frequency, in Hz, followed by an underscore
    
          2.0s - audio length, in seconds
    
          .wav - the extension of the audio format
   


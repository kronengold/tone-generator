'''
tonegen: generate tones based on frequency in Hz provided
'''

import PySimpleGUI as sg
import argparse
import math
import struct
import wave
import sys

#-------------------------------------------------------------------------------
# generate sine_list
#-------------------------------------------------------------------------------
def gen_sine_list(freq, frate, nframes):
    sine_list = []
    for x in range(nframes):
        sine_list.append(math.sin(2.0*math.pi*freq*(x/frate)))
    
    return sine_list

#-------------------------------------------------------------------------------
# save tone to wav file
#-------------------------------------------------------------------------------
def gen_wav(fname, sine_list, freq, frate, amp, nframes):
    nchannels = 1
    sampwidth = 2
    comptype = "NONE"
    compname = "not compressed"

    wav_file = wave.open(fname, "w")
    wav_file.setparams((nchannels, sampwidth, frate, nframes,
        comptype, compname))

    for s in sine_list:
        # write the audio frames to file
        wav_file.writeframes(struct.pack('h', int(s*amp/2)))

    wav_file.close()

    return

#-------------------------------------------------------------------------------
# get arguments
#-------------------------------------------------------------------------------
def get_args():
    parser = argparse.ArgumentParser(
        description='Wave file generator')

    parser.add_argument(
        '-f', '--frequency', \
                help='Set frequency, in Hz', required=False, default=None)
    parser.add_argument(
        '-r', '--framerate', \
                help='Set frame rate of audio file, in frames per second', \
                required=False, default = None)
    parser.add_argument(
        '-t', '--time', \
                help='Set duration of the sound, in seconds', \
                required=False, default=None)
    parser.add_argument(
        '-g', '--gui', help='Display GUI', action='store_true', required=False)

    args = parser.parse_args()

    if (len(sys.argv) == 1):
        print('tonegenGUI -f <frequency> -r <framerate> -t <time> -g')
        print('    f: frequency (Hz), Eg. 440')
        print('    r: frame rate (frames/samples per second), E.g. 41000')
        print('    t: audio length (seconds), E.g. 5')
        print('    g: display dialog box to enter values')
        exit()

    return args

#-------------------------------------------------------------------------------
# get audio parameters
#-------------------------------------------------------------------------------
def get_params(args, params):
    if (args.frequency != None):
        params['Frequency'] = args.frequency
    if (args.framerate != None):
         params['Framerate'] = args.framerate
    if (args.time != None):
         params['Time'] = args.time

    if (args.gui):
        form = sg.FlexForm('NeuroAudit wave file generator')  # begin with a blank form
        layout = [
                [sg.Text('Please enter the following audio parameters')],
                [sg.Text('Frequency [Hz]', size=(20, 1)), sg.InputText(params['Frequency'])],
                [sg.Text('Framerate [Frames/second]', size=(20, 1)), sg.InputText(params['Framerate'])],
                [sg.Text('Time [Seconds]', size=(20, 1)), sg.InputText(params['Time'])],
                [sg.Submit(), sg.Cancel()]
                ]
        button, values = form.LayoutAndRead(layout)

        if button == 'Cancel':
            print('Program cancelled...')
            print("======================================")
            exit()
                    
        if values[0] != '':
            params['Frequency'] = int(values[0])
        if values[1] != '':
            params['Framerate'] = int(values[1])
        if values[2] != '':
            params['Time'] = float(values[2])

    return params

#-------------------------------------------------------------------------------
# main
#-------------------------------------------------------------------------------
def main():

    # sample run: tonegen -f 440 -r 44100 -t 5 -g
    #   f: frequency (Hz)
    #   r: frame rate (frames/samples per second)
    #   t: audio length (seconds)
    #   g: flag for GUI

    params = {'Frequency': '', 'Framerate': '', 'Time': ''}

    print("")
    print("======================================")
    print("Tone Generator")
    print("")

    args = get_args()   # get command line arguments

    params = get_params(args, params)   # get parameters from dialgo box (GUI)

    print("Frequency: {}".format(params['Frequency']))
    print("Framerate: {}".format(params['Framerate']))
    print("Time:      {}".format(params['Time']))
    print("")
    if (params['Frequency'] != '' and params['Framerate'] != '' and params['Time'] != ''):
        filename = str(params['Frequency']) + 'Hz_' + str(params['Time']) + 's.wav'
        amplitude = 64000     # multiplier for amplitude (max is 65,520 for 16 bit)

        nframes = int (params['Time'] * params['Framerate'])

        sine_list = gen_sine_list(params['Frequency'], params['Framerate'], nframes)
        gen_wav(filename, sine_list, params['Frequency'], params['Framerate'], amplitude, nframes)

        print("File {} was saved".format(filename)) 
    else:
        print("Some values are not valid")
    print("======================================")

if __name__ == "__main__":
    main()

# fm_transmitter
Use Raspberry Pi as FM transmitter. Works on any Raspberry Pi board.

This project uses the general clock output to produce frequency modulated radio communication. It is based on idea originaly presented by [Oliver Mattos and Oskar Weigl](http://icrobotics.co.uk/wiki/index.php/Turning_the_Raspberry_Pi_Into_an_FM_Transmitter) on [PiFM project](http://icrobotics.co.uk/wiki/index.php/Turning_the_Raspberry_Pi_Into_an_FM_Transmitter).

## How to use it
To use this project You will have to build it. First, clone this repository, then use "make" command as shown below:
```
git clone https://github.com/markondej/fm_transmitter
cd fm_transmitter
make
``` 
After successful build You can start transmitting by typing:
```
sudo ./fm_transmitter -f 102.0 acoustic_guitar_duet.wav
```
Where:
* -f <frequency> - Specifies the frequency in MHz, 100.0 by default if not passed
* acoustic_guitar_duet.wav - Sample WAVE file, You can use your own

Other options:
* -d <dma_channel> - Specifies the used DMA channel (0 by default), pass 255 in order to disable DMA and use CPU
* -r - Loops the playback

### Supported audio formats
You can transmitt uncompressed WAVE (.wav) files directly or read audio data from stdin, eg.:
```
sox star_wars.wav -r 22050 -c 1 -b 16 -t wav - | sudo ./fm_transmitter -f 100.6 -
```
Please note only uncompressed WAVE files are supported. If You expire "corrupted data" error try converting file, eg. by using SoX:
```
sox my-audio.mp3 -r 22050 -c 1 -b 16 -t wav my-converted-audio.wav
sudo ./fm_transmitter -f 100.6 my-converted-audio.wav
```
### USB microphone support
In order to use a USB microphone input use arecord command, eg.:
```
arecord -D hw:1,0 -c1 -d 0 -r 22050 -f S16_LE | sudo ./fm_transmitter -f 100.6 -
```
In case of performance drop down use ```plughw:1,0``` instead of ```hw:1,0```.

## Legal note
Please keep in mind that transmitting on certain frequencies without special permissions may be illegal in your country.

## New features
* DMA engine support
* works on any Raspberry Pi model
* reads mono and stereo files
* reads data from stdin

Included sample audio was created by [graham_makes](https://freesound.org/people/graham_makes/sounds/449409/) and published on [freesound.org](https://freesound.org/)
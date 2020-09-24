# nametweaker
Tweak the name and other user settings on Leapfrog MyOwnLeaptop devices

Background: See https://www.reddit.com/r/OpenLF/comments/a7n0et/how_to_access_usb_mass_storage_on_a_my_own/

## Scripts
* changename.py: Changes the user name and sound file on the Leaptop device.
* nametweaker.py: Interactive utility to work with Leaptop ROM images.

### changename.py
Usage: `python3 changename.py <new_name> <new_sound_file>`
* `<new_name>` - New user name, limited to 8 characters.
* `<new_sound_file>` - Audio file (path) of recorded name in [WAV](https://en.wikipedia.org/wiki/WAV) or [MP3](https://en.wikipedia.org/wiki/MP3) format

Example: `python3 changename.py jane jane.mp3`

### nametweaker.py
Make sure the Leaptop is connected to your computer before running the nametweaker script.

Usage: `python3 nametweaker.py`

Once started type `help` for more commands.

## Name Recording Files
Leapfrog still has a repository of name recording files available online. Alternatively you can record your own or use any recorded WAV or MP3 file that is small enough.

MP3s of the stock Leapfrog name recordings can be retrieved via `http://lfccontent.leapfrog.com/myname/audio/en_us/preview/NOM_xxxx.mp3`, where `xxxx` is a number.

To find the correct number for a particular name use a web browser and go to http://lfccontent2.leapfrog.com/myname/index.html, find the name and click on the sound preview icon next to the name. The link will not work but look in the URL bar of the browser toward the end and it will have something like "NOM_3053.mp3" - that number is the one you want.

## Ubuntu 18.04 LTS Instructions
Instructions for Ubuntu. This can work in a virtual machine (VMWare tested). Execute the following from a terminal window. The example uses the name 'jane' (Leapfrog audio recording NOM_1416.mp3).

```
sudo apt update
sudo apt upgrade
sudo apt install git python3-pydub sg3-utils wine64 winetricks
winetricks -q mfc42
git clone https://github.com/mac2612/nametweaker.git
cd nametweaker
wget -O jane.mp3 http://lfccontent2.leapfrog.com/myname/audio/en_us/preview/NOM_1416.mp3
```

Connect the Leaptop to your computer via USB and turn it on. Then run the changename.py script.
```
python3 changename.py jane jane.mp3
```

Turn off the Leaptop, disconnect it from the computer and turn it back on. The Leaptop should boot and say the updated name.

If the name recording is too loud here is a tweak to lower the volume of the mp3 file to 70% of the original (adjust as necessary). The example below uses the name 'jane' but use the correct file from your download:
```
sudo apt install sox lame libsox-fmt-mp3
mv jane jane-orig.mp3
sox -v 0.7 jane-orig.mp3 jane.mp3
```

Now use the new jane.mp3 file as an argument to the changename.py script in the above instructions.

- [OctoPi and OctoPrint Mini Guide](#octopi-and-octoprint-mini-guide)
  * [What You Need For OctoPi](#what-you-need-for-octopi)
  * [Setup OctoPi](#setup-octopi)
    + [Download and Flash OctoPi](#download-and-flash-octoprint)
    + [Setup Wi-Fi](#setup-wi-fi)
    + [Power up your OctoPi server](#power-up-your-octoprint-server)
    + [Command Line Setup](#command-line-setup)
  * [Setup OctoPrint](#setup-octoprint)
    + [OctoPrint Setup (web interface)](#octoprint-setup--web-interface-)
      - [Print bed & build volume](#print-bed---build-volume)
      - [Axes](#axes)
      - [Hot end & extruder](#hot-end---extruder)
    + [Connect PrusaSlicer to OctoPrint](#connect-prusaslicer-to-octoprint)
  * [OctoPrint Plugins](#octoprint-plugins)
    + [Essential Plugins](#essential-plugins)
  * [Common Issues](#common-issues)
    + [I connect to my mini using USB](#i-connect-to-my-mini-using-usb)
    + [Performance issues, bad 3d prints, something is wrong](#performance-issues--bad-3d-prints--something-is-wrong)
  * [Sources](#sources)

# OctoPi and OctoPrint Mini Guide
A complete guide for setting up OctoPi and Octoprint for the Prusa Mini. While this guide is biased towards OctoPi -- which packages OctoPrint, mjpg-streamer, and more for the raspberry pi -- if you want to use OctoPrint on another platform feel free to skip to the OctoPrint setup instructions after installation.  

## What You Need For OctoPi
This guide will be more useful if you have all the equipment required. Here is a list:

- [ ] Prusa Mini 3D Printer
- [ ] Raspberry Pi (Raspberry Pi A, B, A+, B+, 2B, 3A+, 3B, 3B+, 4B 1/2/4GB, don't bother with zero models) w/ a power cord. You should really only consider the Pi3B+ or 4B Models.
- [ ] SD card (the bigger then better, especially if you have a camera)
- [ ] A USB or raspberry pi compatible camera (optional but highly recommended)
- [ ] A USB A to USB micro cord

## Setup OctoPi
These are instructions specific to setting up OctoPi

### Download and Flash OctoPi

1. Download the Etcher applicatoin to flas the SD card: https://www.balena.io/etcher/
2. Go to https://octoprint.org/download/ and download the latest OctoPrint image.
3. Insert your SD card into your computer.
4. Open Etcher
    - Click on "Flash from file" and select your newly downloaded OctoPrint image.
    - Click on "Select target" and select the sd card drive.
    - Click on "Flash!" and wait until flash drive is finished.

### Setup Wi-Fi
If you plan on using ethernet, skip this step.

1. Download the Sublime Text Editor: https://www.sublimetext.com/3
2. On your computer navigate to the newly flashed SD card. There will be a file called ```octopi-wpa-supplicant.txt```. Open this in sublime text.
3. Change the WPA 2 section with your SSID and Wi-Fi password (at least you should be using this vs WEP or no security). This is shown below.
4. Save ```octopi-wpa-supplicant.txt``` and close sublime text.

__Before__
```
## WPA/WPA2 secured
#network={
#  ssid="put SSID here"
#  psk="put password here"
#}
```
__After__
_This assumes the wi-fi network you are connecting to is called "YourWifi" and the password to connect to it is called "yourwifipassword"_
```
## WPA/WPA2 secured
#network={
#  ssid="YourWifi"
#  psk="yourwifipassowrd"
#}
```
Go here for more detailed instructions: https://community.octoprint.org/t/wifi-setup-and-troubleshooting/184

### Power up your OctoPi server
In order to setup OctoPrint it's time to power it up.

1. Remove the mini sd card from your computer and insert it into your raspberry pi. 
2. Connect power to your raspberry pi.

### Command Line Setup
This will setup some system level settings (Linux):

1. Log into your Pi via SSH (it is located at octopi.local if your computer supports bonjour or the IP address assigned by your router), 
    - default username is “pi”, default password is “raspberry”. 
2. Run ```sudo raspi-config```. Once that is open:
3. Change the password via “Change User Password”
4. Change the configured timezone via “Localization Options” > “Timezone”.

## Setup OctoPrint
Now it's time to setup OctoPrint specific to you. This includes setting up better security, your mini printer, etc. First we start with the command line, then we will complete the setup using the OctoPrint web interface.

### OctoPrint Setup (web interface)
Finally we are ready to setup your Mini printer with OctoPrint

#### Print bed & build volume

| Setting Name | Prusa Mini Value |
| --- | --- |
| Form Factor | Rectangular |
| Origin | Lower Left |
| Heated Bed | true |
| Heated Chamber | false |
| Width (X) | 180mm |
| Depth (Y) | 180mm |
| Height (Z) | 180mm |
| Custom Bounding Box | true |
| X Coordinates | 0 / 180 |
| Y Coordinates | -4 / 180 |
| Z Coordinates | 0 / 180|

#### Axes

| Setting Name | Prusa Mini Value |
| --- | --- |
| X | 10800 mm/min |
| Y | 10800 mm/min |
| Z | 720 mm/min |
| E | 4800 mm/min |

#### Hot end & extruder

| Setting Name | Prusa Mini Value |
| --- | --- |
| Nozzle Diameter | 0.4 mm |
| Number of Extruders | 1 |

### Connect PrusaSlicer to OctoPrint
* On OctoPrint, go to Settings (wrench icon) > Features > API and copy the API Key
* In PrusaSlicer, go to the “Printer Settings” tab and switch the “Advanced” or “Expert” configuration levels.
    * Under “General” modify the “Print Host upload” with the following settings:
        * Hostname, IP or URL: octopi.local (or whatever you modified it to be)
        * API Key/Password: The API key you copied above
        * Save as a new profile and use this whenever you want to be able to directly upload to the printer.

## OctoPrint Plugins
Plugins allow developers to expand the base functionality of OctoPrint. There are at least a couple of plugins that should be considered essential for mini owners. Each plugin can consume addition resources which can result in degraded printing performance if OctoPrint is slow to send the current g-code instructions over the serial connection as a result of your raspberry pi's CPU being too high. 

### Essential Plugins
Here are the plugins you should defenitley install:

| Plugin Name | Description |
| --- | --- |
| [PrusaSlicer Thumbnails](https://github.com/jneilliii/OctoPrint-PrusaSlicerThumbnails) | This plugin will extract the embedded thumbnails from PrusaSlicer gcode files where the printer's profile ini file has the thumbnail option configured. This is default behavior for the Prusa Mini printer profile. |
| [OctoPrint-Prusa-Mini-ETA](https://github.com/vookimedlo/OctoPrint-Prusa-Mini-ETA) | This plugin will provide ETA estimates, which are broken with the base installation |

## Common Issues
This attempts to answer common issues that mini owners have experienced.

### I connect to my mini using USB
This seems to be a common issue and is probably related to the Mini's slightly recessed usb port. The theory is that a lot of cables do not work well because cannot make contact with the recessed port. Some users have reported trying four USB cables before they found one that was able to connect properly.

### Performance issues, bad 3d prints, something is wrong
Restart your OctoPrint instance in safe mode. This will start it without all the plugins. Then try the same print job, etc, and see if the problems persist. Almost all problems are caused by plugins. 
    
## Sources
* [Julia's Docs](https://docs.juliaebert.com/3d-printing/octoprint)
* [Cable Issues - Prusa Forums](https://forum.prusaprinters.org/forum/user-mods-octoprint-enclosures-nozzles/prusa-mini-and-octoprint/#post-225129)
* [What is the difference between OctoPrint and OctoPi? Are they the same thing?](https://community.octoprint.org/t/what-is-the-difference-between-octoprint-and-octopi-are-they-the-same-thing/185)

# OctoPrint Mini Guide
A complete guide for setting up Octoprint for the Prusa Mini.

## What You Need
This guide will be more useful if you have all the equipment required. Here is a list:

- [ ] Prusa Mini 3D Printer
- [ ] Raspberry Pi (Raspberry Pi A, B, A+, B+, 2B, 3A+, 3B, 3B+, 4B 1/2/4GB, don't bother with zero models) w/ a power cord. The faster the model the better.
- [ ] SD card (the bigger then better, especially if you have a camera)
- [ ] A USB or raspberry pi compatible camera (optional but highly recommended)
- [ ] A USB A to USB micro cord

## Setup
Now it's time to set it up.

### Download and Flash Octoprint

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
2. On your computer navigate to the newly flashed SD card. There will be a file called ```octopi-wpa-supplicant.txt```. Open this in sublime.
3. Change the WPA 2 section with your SSID and Wi-Fi password (at least you should be using this vs WEP or no security). 

### Setup OctoPrint


## Common Issues

1. a

  2. b
  
    3. c

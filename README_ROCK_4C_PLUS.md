# Using an Argon 40 ONE V2 case with a ROCK 4 C+

Because of compatible layout, an Argon40 ONE V2 case can be used with a ROCK 4 C+ board. This document
descibes how.

## Hardware

Because the cpu of the ROCK is not at the same place as it is on Raspberry 4b and has a lower
profile, one need to remove about 0.5mm of the heat sink that would touch the CPU. Just use a slim taper
file but be sure all metal filligs will be removed.

## Software

The Argon cases detects power down by monitoring the UART. It must be enabled, as well as I²C to
communicate with the MCU.

For ARMBIAN, add

overlays=i2c7 uart4

to /boot/armbianEnv.txt

### Building libmraa

On Debian (Armbian), install dependencies first:

apt install build-essential libgtk-3-dev libudisks2-dev libglib2.0-dev cmake swig

clone libmraa WITH Radxa patches

git clone https://github.com/xt3firm/mraa.git

Note: This repository contains the Radxa patches on top of current mraa, should build file with Debian 11 and 12.

Build mraa

mkdir build && cd build
cmake .. && make -j 6

If all went smoothly, install libmraa

make install

### Installing argononed with mraa support

Install the argon service, argononed.py. Replace /usr/bin/argononed.py with examples/C/argononed from the mraa build. Restart the argononed service. Done.

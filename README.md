Overview
========

A demonstration of a Pico reading auto from a PCM1804 A/D converter 
via an I2S bus. The I2S protocol is implemented using the Pico PIO
mechanism.  

Notes
=====

## Regarding Clock Speeds

* We are running the Pico at 125 MHz
* The I2S SCK runs at Fs * 384 (configured on the PCM1804)
* The Pico PIO state machine that generates the SCK needs to run at 2x the SCK speed
because each toggle requires two instructions.
* In order to minimize clock jitter, we want to use an integer divisor 
to reduce the Pico system clock to the Pico PIO state machine clock. A divisor of 4 is chosen in this case.
* Working through the math, this results in an Fs of around 40,690 Hz. This isn't exactly a standard audio speed, but it's close enough.

References
==========

Pico Datasheet: https://datasheets.raspberrypi.com/rp2040/rp2040-datasheet.pdf
PCM1804 Datasheet: https://www.ti.com/lit/ds/symlink/pcm1804.pdf
I2S Protcol Spec (NXP): https://www.nxp.com/docs/en/user-manual/UM11732.pdf

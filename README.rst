ESP32-NESEMU, a Nintendo Entertainment System emulator for the ESP32
====================================================================

This is a forked version of ESP32-NESEMU so that it can be run without changes on an IoT-Bus Io plugged into an IoT-Bus Display.

This is a quick and dirty port of Nofrendo, a Nintendo Entertainment System emulator. Sound does work but not great quality, but can emulate a NES at close
to full speed, albeit with some framedrop due to the way the display is driven.

Warning
-------

This is a proof-of-concept and not an official application note. As such, this code is entirely unsupported by Espressif.


Compiling
---------

This code is an esp-idf project. You will need esp-idf to compile it. 

Display
-------

To display the NES output, please plug an IoT-Bus Io into an IoT-Bus Display. Pins used are:

    =====  =======================
    Pin    GPIO
    =====  =======================
    MISO   19
    MOSI   23
    CLK    18
    CS     5
    DC     27
    RST    NA
    BCKL   33
    =====  =======================

Ground and 3V3 are also connected. EN is connected to TFT RESET.    

(BCKL = backlight enable)

For now, the LCD is controlled using a SPI peripheral, fed using the 2nd CPU. This is less than ideal; feeding
the SPI controller using DMA is better, but was left out due to this being a proof of concept.

Controller
----------

To control the NES, connect a Playstation 1 or 2 controller as such:

    =====  =====
    Pin    GPIO
    =====  =====
    CLK    15
    DAT    14
    ATT    13
    CMD    4
    =====  =====

Also connect the power and ground lines. Most PS1/PS2 controllers work fine from a 3.3V power supply.

ROM
---
This NES emulator does not come with a ROM. Please supply your own and flash to address 0x00100000. You can use the flashrom.sh script as a template for doing so.
You can download ROMs from multiple locations on the web.

Copyright
---------

Code in this repository is Copyright (C) 2016 Espressif Systems, licensed under the Apache License 2.0 as described in the file LICENSE. Code in the
components/nofrendo is Copyright (c) 1998-2000 Matthew Conte (matt@conte.com) and licensed under the GPLv2.


This file is a README file for the 1-Wire library for TiDE, containing
directions, how to use the library.

1. Overview

This library is intended to be used as a transparent bridge between PIC
tibbit (#31) and 1-wire bus. The library contains two parts: the TPS-based code,
which must be included in your project, and PIC firmware which must be uploaded
to the PIC memory prior any operation.

Additionally, the library contains sample code to discover and poll widely used
DS18B20 digital thermometers, manufactured by Maxim Integrated. You can examine
the code and read comments to understand how library functions is utilized.

A basic knowledge of 1-wire protocol internals and electrical characteristics
is strongly recommended. You can navigate to

https://www.maximintegrated.com/en/app-notes/index.mvp/id/1796

to find more about the 1-wire technology.

2. How to use this library

2.1 Prerequisites

To compile and use this library, you will need the Tibbo Project PCB 2/3,
Gen 1 or Gen 2, Tibbit #31 (PIC coprocessor) and (optionally) Tibbit #00-3 if
you plan to power sensors from TPB. To wire the sensors to the TPB, you can
use either Tibbit #20 (9 terminal blocks) or Tibbit #21 (4 terminal blocks).
Also, you need to have the latest version of Tibbo IDE (TiDE) to be installed
on your computer.

2.2 Hardware

Typical layout of the tibbits on the board is shown in the picture below:

                        +--------+--------+
                        |        |        |
                        |        |        |
                        |   31   |  00-3  |
                        |        |        |
                        |        |        |
                        +--------+--------+
                        |       20        |
                        +--------+--------+

This layout is very handy when you plan to power sensors from board internal
power source. Tibbit #20 allows you to take both +5VDC and Ground right near
the 1-wire bus contacts.

Pins on the Tibbit #20 counted from left to right. Pins 1, 2 and 3 is three
1-wire independent channels, pins 5 and 9 is a system ground, and pin 8 is
+5VDC. Pins 6 and 7 is direct I/O lines (its numbers depends on the
Tibbit #00-3 location).

Depending on how many of sensors you plan to connect to the bus, you may need
to install pull-up resistor (120 Ohm) between +5VDC and signal wire, but for
about of 8-10 sensors, this step is not necessary.

2.3 Software

The TPS-based part of the library is written in Tibbo Basic and consists of two
header files and two source files: 1-wire.tbs (1-wire.tph) and PIC_LVP.tbs
(PIC_LVP.tbh)

* 1-wire.tbs/1-wire.tbh contains 1-wire related functions and procedures. Add
this files to your project; this is an essential component of the library.

* PIC_LVP.tbs/PIC_LVP.tbh is complementary files, containing functions and
procedures which are used to aid in uploading firmware into the PIC tibbit
memory. Firmware uploading must be done once; after then firmware will reside
in the PIC program memory, even if the power is switched off. Also, this source
file contains utility functions to help detection of the PIC tibbit presence in
the specified slot and determining which model it is and which version of
firmware it runs.

* i2c_1wire_bridge.hex is a compiled firmware code. If you interested in the
firmware source code itself, look into the "fw" subdirectory for the file
"i2c_1wire_bridge.asm". You will need MicroChip's MPLAB X IDE to compile this
file.

If you do not plan to support firmware uploading in your project, you can remove
PIC_LVP.tbs, PIC_LVP.tbh, and firmware hex file from your project.

* main.tbs file contains source code of the sample project.


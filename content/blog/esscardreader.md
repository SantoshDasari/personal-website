---
title: Engineering Students' Society Card Reader
date: 2020-03-29T05:00:00.000+00:00
author: Ratik Kapoor
image: images/cardReader.png
description: The development of the ESS Card Reader

---
In order to better engage students at the Schulich School of Engineering, I created a points system and the accompanying card reader, which allows students to collect points by coming to events.

The device is powered by a Raspberry Pi Zero W, which is running a custom Linux operating system and kernel that I designed. This was done using [Buildroot](https://buildroot.org "Buildroot"), a tool to create embedded Linux systems with very little overhead. My main issue with Raspbian (the default OS for Raspberry Pi's) was that each boot took almost two minutes. There was simply too much overhead for such a small project. Creating my own OS (with Linux kernel tweaks) allowed me to optimize this to a solid seven second boot, allowing me to start the device a whopping \~17x faster. This. however, presented it's own challenges as a build environment is not available on the target device. As such, I was forced to cross compile many of the libraries and dependencies that I used straight into the OS ([example](https://github.com/RatikKapoor/buildroot_python_adafruit_blinka "Example")). Below is an image of the linux kernel configuration screen from when I was developing this build:

![](https://ratik.me/images/buildroot.png "Linux Kernel Config for Raspberry Pi Zero W")

{{< center >}}Linux Kernel Config for Raspberry Pi Zero W{{< /center >}}

On top of that, I have an RFID module, an LCD display, and buttons connected to the Raspberry Pi pins. I also designed the circuit board used in the project. This was done in started in CircuitMaker but I eventually finished the board in Altium:

![](https://ratik.me/images/cardReaderCircuitDesign.jpg "Designing the PCB to house all components")

{{< center >}}Designing the PCB to house all components{{< /center >}}

Afterwards, I got the PCBs produced from the design and soldered all the components.

The main program was written in Python, and uses OAuth2 for securely connecting to G Suite APIs. This allows the data for each user to be stored in a protected Google Sheets file. An advantage to this system is being able to simply view and update records using Sheets and the card reader will automatically update everything. Since we have over 900 members, this allows for easier and more secure data processing. I also designed the RFID cards and got them manufactured. Here are some pictures of the project in development:

![](https://ratik.me/images/cardReaderDebugging.jpg "Debugging main program")

{{< center >}}Debugging main program after WPA-supplicant kernel panics{{< /center >}}

![](https://ratik.me/images/cardReaderBreadboard.jpg "Testing program with hardware on breadboard and custom designed card")

{{< center >}}Testing program with hardware on breadboard and custom designed card{{< /center >}
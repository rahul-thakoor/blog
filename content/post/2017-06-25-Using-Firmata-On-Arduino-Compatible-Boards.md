---
title: Using Firmata On Arduino Compatible Boards
date: 2017-06-25 08:12:00
categories:
- blog
tags:
- NodeBots
- Johnny-Five
- Maker
- DIY
- Firmata
layout: post

description: Using Firmata On Arduino Compatible Boards
author: rahul
externalLink: false
---

## What is Arduino?
Arduino is an open-source electronics prototyping platform. An Arduino board is development hardware consisting of a programmable microcontroller. The boards can collect information(inputs), act on the inputs(processing) and finally produce outputs. Typically, Arduino boards are programmed using the Arduino programming language through the Arduino IDE using custom firmware(sketches). Arduino exists in many forms and flavours, from the official boards such as the UNO, ArduinoBoard 101 and MEGA, to Arduino-compatible ones like the NodeMCU.

![Components](https://github.com/rahul-thakoor/kws/raw/master/firmata%20on%20arduino/arduino.jpg)


   

## Firmata
Arduino boards are usually based on microcontrollers with low CPU clock speed (around 16 to 32 MHz) and limited memory space. The Firmata protocol provides a way to harness the power of a more powerful machine to run complex processing while using the arduino being used to collect data from sensors and execute desired outputs.

Firmata is a protocol allowing communication between software and microcontrollers. It thus provides a common language with which both the software and hardware can communicate. It works as a host-client method where the microcontroller acts as the client and a more powerful device (smartphone, tablet or computer) acts as the host communicating through a channel such as WiFi, Bluetooth or USB connection. Basically, Firmata makes the board Input/Output pins available via serial communication.

The protocol has two implementations : Firmware and Client Libraries.
The firmware runs on the development board and establishes a method for communication with software running on a host machine. The Arduino IDE provides a Firmata library, implementing the Firmata protocol.

The client libraries are software implementation of the Firmata protocol running on the host machine. Several Firmata client libraries and frameworks have been implemented in a variety of popular programming languages, namely Processing, Javascript, Python, Java and even Go! 

![Components](https://github.com/rahul-thakoor/kws/raw/master/firmata%20on%20arduino/firmata%20protocol.jpg)

### Advantages
* The protocol can be implemented in firmware on any microcontroller architecture
* The protocol can be implemented in software in any programming language
* The host machine runs the program logic and is not limited in resources like the microcontroller
* The microcontoller is able to communicate with different host machines - it does not run a single-purpose program
* No compilation is needed to run the program - just start another script on the host machine

### Disadvantages

* The board depends on the host machine - it can only operate as long as the host machine is running the software
* The board may need to be constantly powered on

## Connectivity

The client hardware can be connected to the host machine either physically (through a cable) or wirelessly. There Arduino IDE provides different implementations of the firmware taking into consideration the different means of communication such as Serial, Ethernet, WiFi and Bluetooth.

## Getting Started on Arduino-Compatible Boards

### Flashing Firmata Firmware

Download and install the <a href="https://www.arduino.cc/en/Main/Software" target="_blank">Arduino IDE</a>.

Arduino provides Firmata as sketches. The StandardFirmata sketch is the most widely used. It allows communication via a serial port such as USB.
To flash it, naviagte to File --> Examples --> Firmata --> Standard Firmata. Choose the appropriate options for your board in the Tools section and finally upload the sketch to the arduino board.

![Components](https://github.com/rahul-thakoor/kws/raw/master/firmata%20on%20arduino/arduino-firmata-library.png)

### Testing
#### Via Firmata Test Program

Firmata provides a test program for boards running StandardFirmata. It allows quick testing of all I/O pins. It runs without installation and works on Windows, MacOs, and Linux. The binaries can be found <a href="https://github.com/firmata/firmata_test/downloads" target="_blank">here</a>.

![Components](https://github.com/rahul-thakoor/kws/raw/master/firmata%20on%20arduino/firmata_test.png)

#### Via Education LAB for Arduino and Firmata by Quai-Lab

It is similar to the Firmata Test program, however it is available as a chrome extension.
It has a RECORDER feature that enables the recording and the replay of the actions done with the interface and an OSCILLOSCOPE feature which allows to observe voltage changes on one of the analog input.

![Components](https://github.com/rahul-thakoor/kws/raw/master/firmata%20on%20arduino/education-lab.png)

### Writing Software

Once the board running Firmata firmware has been tested, software can be implemented in different programming languages. There are different client libraries.

![Components](https://github.com/rahul-thakoor/kws/raw/master/firmata%20on%20arduino/pymata.png)


Also, there are frameworks using the libraries which makes it easier to write software for the board. The most popular frameworks use Javascript and include Johnny-Five and Cylon.Js.

![Components](https://github.com/rahul-thakoor/kws/raw/master/firmata%20on%20arduino/j5-blink.png)


## References
1. Arduino, <a href="https://www.arduino.cc/" target="_blank">https://www.arduino.cc/</a>
2. Firmata Procotol, <a href="https://github.com/firmata/protocol" target="_blank">https://github.com/firmata/protocol</a>
3. Firmata Test Program, <a  href="https://github.com/firmata/firmata_test" target="_blank">https://github.com/firmata/firmata_test</a>
4.  Education LAB for Arduino and Firmata, <a  href="http://quai-lab.com/lancement-deducative-lab-arduino/" target="_blank">http://quai-lab.com/lancement-deducative-lab-arduino/</a>
5. Johnny-Five Framework, <a href="http://johnny-five.io/" target="_blank">http://johnny-five.io/</a>
6. Cylon.JS, <a  href="https://cylonjs.com/" target="_blank">https://cylonjs.com/</a>
7. Lyza Danger Gardner, JavaScript on Things - Chapter 1, <a  href="https://www.manning.com/books/javascript-on-things" target="_blank">https://www.manning.com/books/javascript-on-things</a>

---
title: "Physical Computing With Rust On Raspberry Pi"
subtitle: "Use Rust to control LEDs, Buzzers, and more with the Raspberry Pi"
date: 2018-07-07T23:06:32+04:00
draft: false
---

A couple of months ago I released the `rust_gpiozero`[^1] crate. It is a port of the GPIO Zero[^2] library by the Raspberry Pi Foundation. The library provides a simple interface to control GPIO devices with a Raspberry Pi. I recently ported the Raspberry Pi Foundation's "Physical Computing with Python"[^3] guide for Rust. 

## Why did I create the `rust_gpiozero` crate?

After going through "The Rust Programming language" book, I decided to work on a side project to practice some of the concepts. I enjoy working with microcontrollers and Single Board Computers and making beginner tutorials. I looked for crates related to the raspbery Pi and controlling GPIO pins and came across several great ones such as `rppal`, `sysfs_gpio` and `i2cdev`. The idea behind `rust_gpizero` was to abstract away some of the complexities and provide a high-level interface to experimenting with GPIO pins on the Raspberry Pi using Rust. This is similar to the original python based GPIOZero library which uses the `RPi.GPIO` library under the hood. You can experiment with very little code. I also tried to keep a similar API to the original `GPIOZero` library. 

>Blinking an `LED` using `GPIOZero`

<figure>
  <img src="/img/physical-computing-rust-python-example.png" alt="Lighting an LED using Python" style="width:80%">
  <figcaption style="font-size:12px;text-align:right">Generated using: <a href="https://carbon.now.sh/" target="_blank">carbon</a></figcaption>
</figure>

<!-- ```python
from gpiozero import LED
from time import sleep

led = LED(17)

while True:
    led.on()
    sleep(1)
    led.off()
    sleep(1)
``` -->

>Similarly, blinking an `LED` using `rust_gpiozero`

<figure>
  <img src="/img/physical-computing-rust-example.png" alt="Lighting an LED using Python" style="width:80%">
  <figcaption style="font-size:12px;text-align:right">Generated using: <a href="https://carbon.now.sh/" target="_blank">carbon</a></figcaption>
</figure>

<!-- ```rust
extern crate rust_gpiozero;
use rust_gpiozero::*;
use std::thread::sleep;
use std::time::Duration;

fn main() {

let mut led = LED::new(17);

loop{
    led.on();
    sleep(Duration::from_secs(1));
    led.off();
    sleep(Duration::from_secs(1));
    }
}
``` -->

The library is still a work-in-progress and there are many improvements which can be made. 

## Tutorials to accompany the crate

**Physical Computing with Python** (published under a Creative Commons license) by The Raspberry Pi Foundation is a great guide which introduces physical computing. The guide uses `GPIOZero` and teaches how to interface with electronic components such as LEDs, Buzzers and Sensors. More importantly, the guide 
_covers elements from the following strands of the Raspberry Pi Digital Making Curriculum[^4]:_

+ _Use basic programming constructs to create simple programs_
+ _Use basic digital, analogue, and electromechanical components_

<figure>
  <img src="/img/led-gpio17.png" alt="Lighting an LED" style="width:100%">
  <figcaption style="font-size:12px;text-align:right">Source: <a href="https://www.raspberrypi.org" target="_blank">Raspberry Pi Foundation</a></figcaption>
</figure>

I adapted the guide to make **Physical Computing with Rust**. The resource is aimed at those who have some basic programming skills and know some Rust. Ideally, it is recommended to have completed atleast the first three chapters of The Rust Programming Language Book. 

The guide does not _**yet**_ cover all the steps in the original resource.

## Roadmap

As I learn more about Rust, I will continue to improve the `rust_gpio` crate and add corresponding tutorials to the **Physical Computing with Rust** guide. You can contribute to the project by sending PRs, commenting on the code or providing feedback. I intend to learn a lot from the community and any input is much appreciated. Finally, here are some things I wish to implement eventually:

1. Use the Linux GPIO Character Device API instead of sysfs_gpio which has been deprecated since linux 4.4. Paul Osborne is already working on the rust interface[^5].

2. Add background tasks. For e.g, blinking an LED should not block the thread

3. Implement SPI devices API




[^1]: https://crates.io/crates/rust_gpiozero
[^2]: https://gpiozero.readthedocs.io/
[^3]: https://projects.raspberrypi.org/en/projects/physical-computing
[^4]: https://curriculum.raspberrypi.org/
[^5]: https://github.com/posborne/rust-gpio-cdev
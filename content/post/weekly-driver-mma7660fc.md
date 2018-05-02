---
title: "An I2C Rust driver for mma7660fc-based 3-Axis Digital Accelerometer"
date: 2018-05-01T22:44:18+04:00
image: /img/mma7660-driver/grove-accelerometer-back.jpg
categories:
- blog
tags:
- Rust
- Driver
- Embedded
layout: post
description: A platform agnostic driver to interface with the MMA7660FC 3-Axis Accelerometer via I2C using Rust
author: rahul
externalLink: false
---

This is an I2C implementation for mma7660fc-based 3-Axis Digital Accelerometer. It is an [embedded-hal](https://github.com/japaric/embedded-hal) driver as part of the [weekly driver initiative](https://github.com/rust-lang-nursery/embedded-wg/issues/39) by [Jorge Aparicio](https://twitter.com/japaricious).

## The Device

The MMA7660FC is a ±1.5 g 3-Axis Accelerometer with Digital Output
(I2C). It can be found on Seeed's Grove 3-Axis Digital Accelerometer. It is made by NXP Semiconductor.

<div align="center">
<p><img src="/img/mma7660-driver/grove-accelerometer-front.jpg" width ="50%"></p> 
 </div>

## Development

For the development of this driver, I used the Grove 3-Axis Digital Accelerometer and tested on a Raspberry Pi 1 running latest version of [Raspbian](https://www.raspberrypi.org/downloads/raspbian/).

## The Driver
It is quite straightforward to use the driver. The [documentation](https://docs.rs/mma7660fc/0.1.2/mma7660fc/) provides a comprehensive explanation with an example. Essentially:

- Add the [mma7660fc](https://crates.io/crates/mma7660fc) crate as a dependency in the `Cargo.toml` file. You also need an implementation for `embedded-hal`. For Raspberry Pi, I am using [linux-embedded-hal](https://crates.io/crates/linux-embedded-hal).

- Initialise the Linux I2C driver and then create an `Mma7660fc` instance

- Read the accelerometer values

## Conclusion

This is a basic implementation of a driver for mma7660fc-based 3-Axis Digital Accelerometers. The driver does not implement all functionalities. Feedback, suggestions and PR are most welcome. 

## Resources and Links

- [Datasheet](https://www.nxp.com/docs/en/data-sheet/MMA7660FC.pdf)
- [Documentation](https://docs.rs/mma7660fc/)
- [Crate](https://crates.io/crates/mma7660fc)
- [Repository](https://github.com/rahul-thakoor/mma7660fc)

## Acknowledgement

The structure of this post is based on [Danilo Bargen's](https://blog.dbrgn.ch/) weekly driver posts.
---
title: Releasing rust_gpiozero v0.2.0
subtitle: A new version packed with new features and improvements
image: "/img/rust_gpiozero_v0.2.0.png"
date: 2019-02-27 13:43:48 +0000
tags:
- rust
- raspberry pi
- physical computing

---
For the past month I have been working on `rust_gpiozero`. This new release is a complete rewrite and uses [Rene van der Meer(@golemparts)](https://twitter.com/golemparts)'s  `[rppal](https://github.com/golemparts/rppal)` crate under the hood. It also uses Rust 2018 edition.

## Why `rppal`?

Simply because Rene has done an incredible work on `rppal`. It provides first class support for the Raspberry Pis. Instead of trying to (poorly) reimplement the features, I think it is best to build upon the `rppal`. More importantly, Rene just added support for `embedded-hal` drivers which is going to make adding more components to `rust_gpiozero` much easier by leveraging already existing [drivers](https://github.com/rust-embedded/awesome-embedded-rust#driver-crates). You should definitely check out `rppal`.

## What's new?

The main goal for this release was to provide software-based PWM components. At first I experimented with `wiring_pi`. Fortunately, Rene added softpwm  in `[rppal](https://github.com/golemparts/rppal/releases/tag/0.11.0)` v0.11.0 after I requested which made implementing the following components a breeze:

* Adding `speed` feature for `Motor` component
* `PWMOutputDevice`
* `PWMLED`
* `Servo`

There are some API changes in existing components. Also, the `blinking` or `beeping` methods now run in a background thread and do not block the main thread by default.

## Learning Journey

I started `rust_gpiozero` as an educational project and this release was very instructive:

* I worked with threads in Rust which helped me better understand the borrowing, thread safety and closures. I worked with `std::sync::Arc`and `std::sync::Mutex`. However, I think there is still more to learn and discover.
* I used `macro_rules!` for the first time. While previously using `traits`, I felt not being able to override functions and also have access to struct data implementing the traits a challenge. With `macro_rules!`, I organised common implementations accordingly and implemented them where needed. It also made the code _"DRYer"_.
* I got a better understanding of Pulse Width Modulation
* I formatted the code with `rustfmt` and `clippy` ❤️

## What's next?

I am going to write some tutorials on how to use the new features and components. I will also update [Physical Computing with Rust](https://rahul-thakoor.github.io/physical-computing-rust/) to use the new version of `rust_gpiozero`.

I hope to release more new features soon. You can also test the new version and provide feedback.
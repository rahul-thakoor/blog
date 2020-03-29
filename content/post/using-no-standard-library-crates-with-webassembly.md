---
title: Using no standard library crates with Webassembly
date: 2020-03-29T08:00:00+04:00
isCJKLanguage: false
slug: ''
aliases: []
tags:
- embedded
- rust
- wasm
author: ''
subtitle: A Rust + Webassembly experiment using no_std crates
image: "/img/embedded-graphics-web-simulator.jpg"

---
When working with Rust + Webassembly, you might want to use some crates in your project. Not all crates work out of the box with Webassembly yet, especially those that rely on System Libraries, File I/O, Networking, etc. With proposals such as [WASI](https://wasi.dev/ "WebAssembly System Interface") or [WebAssembly Interface Types](https://github.com/WebAssembly/interface-types/blob/master/proposals/interface-types/Explainer.md "WebAssembly Interface Types"), these might work eventually but it isn't the case yet.

The Rust Wasm book suggests:

> A good rule of thumb is that if a crate supports embedded and `#![no_std]` usage, it probably also supports WebAssembly.

## What are no_std crates?

Rust has an extensive standard library and every time you use some functionality, they need to be imported into scope. This can get very verbose and tedious! Rust automatically imports some things into every program and this is known as the prelude. The list of contents to be included in defined in the  `std::prelude` module.

However, when working with Webassembly or Embedded systems, the environment where the code is executed might not have access to System Interface that the std library requires. `#![no_std]` is an attribute that indicates to Rust that the crate will link to the [core crate](https://doc.rust-lang.org/stable/core/index.html "libcore") instead which is a quasi dependency-free and platform-agnostic Rust library defining essential primitives.

The [Rust-Embedded book](https://rust-embedded.github.io/book/intro/no-std.html) has a great explanation about `no_std` environment.

You can find `no_std` crates on [crates.io](https://crates.io/categories/no-std "no_std lib") and the [Awesome Embedded Rust list](https://github.com/rust-embedded/awesome-embedded-rust#no-std-crates).

## An example

![A screenshot of the simulator](/img/embedded-graphics-web-simulator.jpg "Embedded Graphics Web Simulator")

I've been experimenting with Webassembly lately and thought it would be a good educative project to make a [Simulator](https://docs.rs/embedded-graphics-simulator/0.2.0/embedded_graphics_simulator/) that runs on the web for the [Embedded Graphics](https://github.com/jamwaffles/embedded-graphics) by[ James Waples](https://twitter.com/jam_waffles). The library already includes a Simulator but requires installing SDL and its development libraries even to run the demos. With Webassembly we can easily run this on a web page without installing any dependencies! 

Thanks to the awesome work by James and the Rust Wasm team, it was quite trivial to implement this. I created the project using wasm-pack which is great for getting started with Rust + Webassembly work. The Embedded Graphics has great documentation on how to implement a display driver. I implemented the [DrawTarget trait](https://docs.rs/embedded-graphics/0.6.0/embedded_graphics/prelude/trait.DrawTarget.html) for drawing pixels on a `<canvas>` element which in turn the workflow was made great by the `wasm_bindgen`, `js-sys` and `web-sys crates`. 

You can see a [demo](https://rahul-thakoor.github.io/embedded-graphics-web-simulator/) of the built project and find the[ source code on GitHub](https://github.com/rahul-thakoor/embedded-graphics-web-simulator). Feel free to make code reviews or contribute or notify me if I've made mistakes. 

## References

1. [Preludes and no_std](https://doc.rust-lang.org/stable/reference/crates-and-source-files.html?highlight=std#preludes-and-no_std)
2. [Rust Wasm book](https://rustwasm.github.io/docs/book/)
3. The [std::prelude module](https://doc.rust-lang.org/stable/std/prelude/index.html)
4. [wasm-bindgen](https://rustwasm.github.io/docs/wasm-bindgen/)
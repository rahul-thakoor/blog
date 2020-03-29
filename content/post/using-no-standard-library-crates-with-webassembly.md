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
draft: true

---
When working with Rust + Webassembly, you might want to use some crates in your project. Not all crates work out of the box with Webassembly yet, especially those that rely on System Libraries, File I/O, Networking, etc. With proposals such as [WASI](https://wasi.dev/ "WebAssembly System Interface") or [WebAssembly Interface Types](https://github.com/WebAssembly/interface-types/blob/master/proposals/interface-types/Explainer.md "WebAssembly Interface Types"), these might work eventually but it isn't the case yet.

The Rust Wasm book suggests:

> A good rule of thumb is that if a crate supports embedded and `#![no_std]` usage, it probably also supports WebAssembly.

## What are no_std crates?

Rust has an extensive standard library and every time you use some functionality, they need to be imported into scope. This can get very verbose and tedious! Rust automatically imports some things into every program and this is known as the prelude. The list of contents to be included in defined in the  `std::prelude` module.

However, when working with Webassembly or Embedded systems, the environment where the code is executed might not have access to System Interface that the std library requires. `#![no_std]` is an attribute that indicates to Rust that the crate will link to the [core crate](https://doc.rust-lang.org/stable/core/index.html "libcore") instead which is a quasi dependency-free and platform-agnostic Rust library defining essential primitives. 

The [Rust-Embedded book](https://rust-embedded.github.io/book/intro/no-std.html) has a great explanation about `no_std` environment.

You can find no_std crates on [crates.io](https://crates.io/categories/no-std "no_std lib") and the [Awesome Embedded Rust list](https://github.com/rust-embedded/awesome-embedded-rust#no-std-crates). 

## References

1. [Preludes and no_std](https://doc.rust-lang.org/stable/reference/crates-and-source-files.html?highlight=std#preludes-and-no_std)
2. [Rust Wasm book](https://rustwasm.github.io/docs/book/)
3. \[^prelude\]([https://doc.rust-lang.org/stable/std/prelude/index.html](https://doc.rust-lang.org/stable/std/prelude/index.html "https://doc.rust-lang.org/stable/std/prelude/index.html"))
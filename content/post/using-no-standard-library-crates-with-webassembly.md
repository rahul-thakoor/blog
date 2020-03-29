---
title: Using No standard library crates with Webassembly
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
When working with Rust + Webassembly, you might want to use some crates in your project. Not all crates work out of the box with Webassembly yet, especially those that rely on System Libraries, File I/O, Networking, etc. With proposals such as [WASI](https://wasi.dev/ "WebAssembly System Interface") or [WebAssembly Interface Types](https://github.com/WebAssembly/interface-types/blob/master/proposals/interface-types/Explainer.md "WebAssembly Interface Types"), these might work eventually but this isn't the case yet.

The Rust Wasm book suggests:

> A good rule of thumb is that if a crate supports embedded and `#![no_std]` usage, it probably also supports WebAssembly.
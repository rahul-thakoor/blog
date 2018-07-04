---
title: "Rust: Raw string literals"
subtitle: r#"What is this?"#
date: 2018-06-29T22:45:43+04:00
draft: false
tags:
- rust
---

While working with Rust, you will often come across `r#"something like this"#`, especially when working with `JSON` and `TOML` files. It defines a **raw string literal**. When would you use a raw string literal and what makes a valid raw string literal?

## When would you use a raw string literal?

First, let's understand what a string literal is. According to the The Rust Reference[^1], _A string literal is a sequence of any Unicode characters enclosed within two U+0022 (double-quote) characters, with the exception of U+0022 itself[^2]._ Escape characters in the string literal body **are** processed. The string body cannot contain a double-quote. If you need to insert one, you have to escape it like this: `\"`. 

Escaping double-quotes can be cumbersome in some cases such as writing regular expressions or defining a JSON object as a string literal. In these situations, **raw string literals** are helpful since they allow you to write the literal without requiring escapes.

Here is a snippet from the `toml`[^4] crate:
<script src="https://gist.github.com/rahul-thakoor/4c158ef09016973bcc6176c04678e30a.js"></script>

Or another from `serde-rs`[^5]:
<script src="https://gist.github.com/rahul-thakoor/449ea0438a8f6eee39edad0a97204ed9.js"></script>

So, raw string literals are helpful, but what makes a valid one?

## What makes a raw string literal?

The Rust Reference defines a raw string literal as starting  _with the character U+0072 \(r), followed by zero or more of the character U+0023 (#) and a U+0022 (double-quote) character. The raw string body can contain any sequence of Unicode characters and is terminated only by another U+0022 (double-quote) character, followed by the same number of U+0023 (#) characters that preceded the opening U+0022 (double-quote) character._[^3]

Escape characters in the raw string body are **not** processed.

Therefore the following raw string literals are all valid:

<script src="https://gist.github.com/rahul-thakoor/f07fe1a2603fb07a12ca572e639c9328.js"></script>

<a href="https://play.rust-lang.org/?gist=f07fe1a2603fb07a12ca572e639c9328" target="_blank">Try it on playpen</a>

If you need to include double-quote character in a raw string, you must tag the start and end of the raw string with hash/pound signs(`#`).

<script src="https://gist.github.com/rahul-thakoor/3e109456fcdd387c6789c0d3ada68194.js"></script>

<a href="https://play.rust-lang.org/?gist=3e109456fcdd387c6789c0d3ada68194" target="_blank">Try it on playpen</a>

The raw string body can contain any sequence of UNICODE characters except `"#` since it would terminate the literal. If you want to include the particular sequence, you have to change the number of `#` that precede the opening double-quote. For instance:

<script src="https://gist.github.com/rahul-thakoor/2dc72c16c57c4fd594bb648bd30452a4.js"></script>
<a href="https://play.rust-lang.org/?gist=2dc72c16c57c4fd594bb648bd30452a4" target="_blank">Try it on playpen</a>

Likewise, if `"##` is to be included, you can add another `#` to the starting and ending delimiters.  

## Wrap Up

Raw string literals are helpful when you need to avoid escaping characters within a literal. The characters in a raw string represent themselves. _Informally, a raw string literal is an r, followed by N hashes (where N can be zero), a quote, any characters, then a quote followed by N hashes._[^6] 

Here's how visualising[^7] raw string literals works for me:

<figure>
  <img src="/img/rust_raw_string.png" alt="Raw string literal railroad" style="width:100%">
  <figcaption style="font-size:12px;text-align:right">Image generated using Railroad-Diagram-Generator</figcaption>
</figure>



That's it for now! 




[^1]: https://doc.rust-lang.org/stable/reference/

[^2]: https://doc.rust-lang.org/stable/reference/tokens.html#string-literals

[^3]: https://doc.rust-lang.org/stable/reference/tokens.html#raw-string-literals

[^4]: https://github.com/alexcrichton/toml-rs/blob/master/examples/decode.rs

[^5]: https://github.com/serde-rs/json

[^6]: https://github.com/rust-lang/rust/blob/master/src/grammar/raw-string-literal-ambiguity.md

[^7]: http://www.bottlecaps.de/rr/ui


---
title: "My Experience in Increasing Rust's Reach 2018"
date: 2018-09-16T08:49:37+04:00
draft: true
---

I recently had the privilege of participating the Increasing Rust's Reach(IRR) program. The program aims to _grow Rust's community of project collaborators and leaders. Increasing Rust's Reach brings together Rust team members and individuals who are underrepresented in Rust's community and the tech industry for a partnership of three (3) months, from mid-May to mid-August. Each partnership agrees to a commitment of 3–5 hours per week working on a Rust Project._[^1]

The 2018 cohort included 14 participants[^2] , spanning 9 timezones and 11 countries! This year's projects included WebAssembly, `rust-lang.org`'s Design and Internationalisation(Internationalization), Embedded, Diesel, CLI and Clap-rs. I worked on the `rust-lang.org`'s Internationalisation along with Rui Zhao and mentored by Ashley Williams.

![IRR 2018 Participant Map](/img/irr2018-particpant-map.png)

This is my story of how I got into Rust, how the IRR program went and how I intend to keep contributing in the Rust community.

## How I got into Rust
How I got into programming itself and eventually Rust can be a post in itself. I started programming only three years ago(in 2015) while I was studying Medicine in China. I first tried and failed at learning Java on Udacity back in 2012. What followed were several enrollments in numerous courses on different MOOC platforms and eventually abandoning them. I really started learning it again when I bought my first Arduino in 2015. I enjoyed physical computing and learnt a lot by experimenting and building DIY projects. I also realised the importance of documenting and sharing my findings since I was myself learning from a myriad of open educational resources.[^3]

Then in 2016, after completing my medical degree, I decided to officially learn computer science. I decided  to learn Rust after it was chosen as the Most Loved Language in the 2017 Stack Overflow Survey[^4] and _**discovering**_ Jorge Aparicio's book[^5].

After reading the first edition of The Rust Programming Language(TRPL) Book, I decided to start a project of my own to practice the concepts I was learning. Since I like working with microcontrollers and single board computers, I decided to port the awesome python based `GPIOZERO`[^6] library for the Raspberry Pi and made `rust_gpiozero`[^7]. After that I made a driver[^8] for the MMA7660FC 3-Axis Accelerometer based on `embedded-hal` by Jorge Aparicio. I also started contributing on the **Awesome Embedded Rust**[^9] list.

## Increasing Rust's Reach

The program started on 14th May. I had one weekly call with Ashley and one with IRR's participants, mentors and the awesome guests from the Rust community. We had the unique opportunity to interact with guests like Steve Klabnik, Chris Krycho, Carol Nichols Goulding, Sergio Benitez, Santiago Pastorino and more (Sorry for not listing everyone, you are all awesome ❤️). These were all put together by Ashley! Despite still having classes, I aimed to attend all the group meetings since they were very enriching and inspiring. I even attended one using cellular data while traveling on the bus on my way home! 

During the first few weeks, Ashley gave me the opportunity to further my knowledge in Rust. I started reading through the second edition of TRPL book. I decided to work on the **Physical Computing with Rust**[^10] tutorial which is based on the **Physical Computing with Python**[^11] by the Raspberry Pi Foundation and complemented `rust_gpiozero` project. This allowed me to write Rust for the tutorial itself, and also discover `mdbook`[^12]. I also researched and learnt about Internationalization (i18n) and Localization (L10n).

By mid June, we started wrapping up the side projects and started working on the new `rust-lang.org` website.

During the program we sure talked a lot about Rust. However, the program is not only about Rust. I had exposure to diverse ideas either during weekly calls, researching about particular language constructs/syntax, working on the side projects or engaging with the _**awesome Rust community**_ ❤️.

Here are some more ideas I explored or technology I worked with during the program:

- Mozilla Pontoon[^13]
- Fluent[^14]
- Foreign Function Interface
- Cross compilation for the Raspberry Pi
- Making a tool for making publishing crates easier
- Webassembly
- Rocket[^15]
- Raw strings in Rust, I wrote a post[^16] about it
- RFCs
- Traits
- Handlebars.js, SCSS, HTML and Twitter cards

## Going Forward

It was a wonderful experience participating in the IRR program and an absolute delight being mentored by Ashley. Now that the program is over 😔, I will continue learning, contributing and experimenting. Things I'm looking forward to:

1. Continue working on `rust_gpiozero` and develop more tutorials accordingly for **Physical Computing with Rust**
2. Explore Rust across several domains, especially in Webassembly and Embedded by experimenting and doing some proof-of-concept projects and writing tools which may include:
    - Making Rust more accessible on embedded platforms by writing tutorials, developing drivers , hal's or even a framework similar to **Johnny-Five**[^17]
    - Porting some projects I already worked on in different languages to Rust like writing a CHIP-8 emulator[^18], implement some webapps using Rocket, writing a firewall in `eBPF`[^19] and `BCC`[^20] tools, and more
    - Making themes for mdbook
3. Contribute in the Community Team[^21] and Rustbridge[^22] and build a Rust community in my country
4. Understand ownership better and learn advanced topics like Macros, Concurrency, Smart Pointers and more

And yes, I am looking forward to attending Rust Belt Rust 2018 in Ann Arbor, Michigan and finally meet some fellow _rustaceans_ in person.

There is so much to learn and I, for one am eager to discover what lies ahead.


## References

[^1]: [Increasing Rust's Reach](http://reach.`rust-lang.org`/)
[^2]: [IRR 2018 Participants](http://reach.`rust-lang.org`/2018/participants)
[^3]: [My first instructable](https://www.instructables.com/id/ESP8266-ESP-12Standalone-Blynk-101/)
[^4]: [Stack Overflow Developer Survey Results 2017](https://insights.stackoverflow.com/survey/2016#most-loved-dreaded-and-wanted)
[^5]: [Discovery by Jorge Aparicio](https://rust-embedded.github.io/discovery/)
[^6]: [Gpiozero](https://gpiozero.readthedocs.io)
[^7]: [rust_gpiozero](https://crates.io/crates/rust_gpiozero)
[^8]: [mma7660fc](https://crates.io/crates/mma7660fc)
[^9]: [Awesome Embedded Rust](https://github.com/rust-embedded/awesome-embedded-rust)
[^10]: [Physical Computing with Rust](https://rahul-thakoor.github.io/physical-computing-rust/)
[^11]: [Physical Computing with Python](https://projects.raspberrypi.org/en/projects/physical-computing)
[^12]: [mdbook](https://github.com/rust-lang-nursery/mdBook)
[^13]: [Mozilla Pontoon](https://pontoon.mozilla.org/)
[^14]: [Fluent](https://projectfluent.org/)
[^15]: [Rocket](https://rocket.rs/)
[^16]: [Rust: Raw string literals](https://medium.com/@rahulthakoor/rust-raw-string-literals-9579c4feb231)
[^17]: [Johnny-Five](http://johnny-five.io/)
[^18]: [Chip-8](https://en.wikipedia.org/wiki/CHIP-8)
[^19]: [BPF & eBPF](https://en.wikipedia.org/wiki/Berkeley_Packet_Filter)
[^20]: [BCC Tools](https://iovisor.github.io/bcc/)
[^21]: [The Rust Team](https://www.rust-lang.org/en-US/team.html)
[^22]: [Rustbridge](https://github.com/rustbridge/rustbridge.io)
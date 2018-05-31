---
title:  Let's Write an Embedded OS!
categories: [zeptos]
tags: [programming, arm, embedded]
---
A few years ago, someone asked me if I could produce some prototype hardware for a car-sharing project he was starting. At the time, I didn't really have any experience with hardware, PCB design or embedded programming, so of course I said yes.

This guy wasn't putting up any cash at the time—or ever, it would turn out—so I used it as an opportunity to take the time to learn some new skills. I started out with an Arduino 2560, initially using the Arduino environment and libraries to program it. I quickly discovered that the Arduino libraries were designed around a programming concept known as *woeful inefficiency*, and ended up throwing them out, sitting down with a cup of tea and the reference manual, and writing it all from scratch with GCC, a linker script and a Makefile. With several things going on at once (reading from a GPS module, detecting RFID cards, responding to CLI commands, sending telemetry and unlocking car doors), it was clear that it would be far easier if each activity could live in its own process. That meants using an embedded operating system. There are several available, some of which are open source, but why use something already built when you can build your own for five times the effort? (It's no coincidence that I don't write a blog about business acumen.)

## ARM Cortex-M

This also seemed like a good time to switch to using ARM. I'd done a lot of ARM programming in my teens during the 90s (yeah, I was that kind of kid), but this was the first time I'd had a chance to play with the new Cortex-M microcontrollers. Like the AVR microcontollers, they're RISC CPUs with built-in flash storage, static RAM and a bunch of peripherals for talking to the outside world. They're self-contained computers that only need to be connected to power to function. Unlike AVRs, they're 32-bit instead of 8-bit, and significantly more powerful, which is why they've become the new *de facto* standard for small, embedded devices. 

## Zeptos

And so was born Zeptos, named for its minimal functionality.

In this series of blog posts and livestreams, I'll go through that same process of starting from nothing and working up to a basic embedded OS with task switching, message passing and device drivers, which are pretty much the minimum requirements for anything that calls itself an OS. While it would be usual to use a helpful library like mbed or ARM's own CMSIS, the point of this exercise is to get an understanding of everything that's going on under the hood. 

## Blinky!

The "Hello, World!" of embedded programming is getting a single LED to blink. For this series, I'll be using a NUCLEO-F401RE development board, which conveniently has an on-board LED for our use, so we don't have to add any extra hardware. This board is based around an STM32F401 microcontroller from ST Micro, which is an ARM Cortex-M4 device, and has a built-in ST-Link programmer that lets us program the flash memory and use a debugger over USB. It also gives us a virtual serial USB port that we'll be able to use for our debug output. If you want to follow along, you can buy one online for about $10.

In the next part, we'll look at the minimum amount of code needed to get that LED flashing.

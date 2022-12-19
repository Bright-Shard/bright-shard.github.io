---
layout: project
parent: projects.html
title: Hidden HID
github: hidden_hid
---

<!--desc.start-->
An advanced platform-independent tool for invisible HID attacks.
<!--desc.end-->

HiddenHID is a platform-indepdent tool for launching completely invisible HID attacks. It's a simple program that acts as a sort of proxy between a target computer and your BadUSB, granting your exploit superpowers.

# What's an HID Attack?
Computers are dumb, and trust whatever USB device is plugged into them. If you plug a device in, and it tells the computer it's a keyboard, the computer assumes it's a keyboard. If that device instead tells the computer it's a mouse, the computer assumes it's a mouse. If that device says it's a wifi dongle, the computer agrees that it's a wifi dongle. And so on.

This can lead to a pretty simple exploit known as a keystroke injection attack (one kind of HID attack), where you plug a pre-programmed USB device into a computer. (As a sidenote, I'll be using keystroke injection & HID attack interchangeably, though they are different. Keystroke injection attacks abuse keyboards and keystrokes, while HID attacks are a wide range of attacks that abuse Human Interface Devices, or HIDs - including mice, wifi dongles, keyboards, etc.) The pre-programmed USB device (Commonly called a "BadUSB") tells the computer it's a keyboard, and, because it's pre-programmed, can "type" programmed keystrokes at superhuman speeds. It can type anything on a keyboard, from the letter A to the Windows key. BadUSBs can also use keyboard shortcuts by "typing" multiple keys at the same time.

This sounds kind of minor, until you realize how powerful keyboard shortcuts are. Keyboard shortcuts can open apps - *any app* - including terminals, web browsers, password managers, messaging apps...

![Explosion GIF](https://tenor.com/view/yeah-csi-miami-glasses-sunglasses-horatio-caine-gif-14033607.gif)

Keystroke injection attacks are terrifying. They can abuse keyboard shortcuts to open any app on the system, including the terminal, as mentioned before. Because of this, they can do basically *anything* to your computer - all from a little device that looks like a USB thumbdrive.

## Examples
You can see some examples here:

- [https://www.youtube.com/watch?v=7YpJQT55_Y8](https://www.youtube.com/watch?v=7YpJQT55_Y8)
- [https://www.youtube.com/watch?v=uH-4btjE56E](https://www.youtube.com/watch?v=uH-4btjE56E)
- [https://www.youtube.com/watch?v=meNlOrdQJFo](https://www.youtube.com/watch?v=meNlOrdQJFo)

# Issues with HID Attacks
There's only really three faults to keystroke injection attacks:
1. Visibility: Because they act like keyboards, and open apps, everything in an HID attack is visible to the target. *Painfully* visible. This means you usually can only use these at unattended computers.
2. Platform-specific: Because they use keyboard shortcuts and (usually) type commands in a terminal, almost every payload for an HID attack has to be re-written for different platforms. Windows, macOS, and Linux all have different keyboard shortcuts for different things, besides the major differences in their terminal commands.
3. One-way communication: The keyboard can talk to a computer, but not really the other way around. This means you have to get very creative in order to receive data back from the computer.

# A Grand Solution - HiddenHID
HiddenHID aims to solve all three of the above problems.

First, HiddenHID can abuse opacity settings to render as a *completely transparent* app window. It comes with a textbox - also completely transparent - that can act as a terminal. This means that HID attacks can run on a computer while being completely hidden (hence the name).

Second, HiddenHID comes bundled with BrightScript, a "programming language" intended for HID attacks. It's simple, but effective, and can automate many redundant tasks in HID attacks. BrightScript is platform-independent, meaning only one payload is needed to run on any device.

Finally, HiddenHID can talk back to your BadUSB via serial communication. This means you can both send data to a target computer *and* get data back. This unlocks the possibility for dynamic exploits that change how they execute on the fly. This isn't possible with normal HID attacks that can only talk to the computer - or, at least, it's *very difficult* to do.

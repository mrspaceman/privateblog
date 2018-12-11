---
author: aaspellc
layout: default_post
title: Windows Subsystem for Linux Internals
summary: "A description of the windows subsystem for linux architecture"
categories:
  - Tech
image: aaspellc/assets/windows-arch.png
tags: 'Linux, Operating Systems'
---

{% assign root_url = site.github.url %}
{% assign root_url = site.github.url/aaspellc %}
{% assign root_url = "/privateblog" %}

# Windows Subsystem For Linux Internals

## Background

Windows Subsystem for Linux was developed by Microsoft to enable command line
programs compiled for the Linux operating system to be executed on Windows.

To explain the architecture I would like to show the evolution of OS design and how
that has enabled this subsystem to be built.

## Dark Ages (or Back in the Day)

Microsoft's MS-DOS was quite primitive in it's design (compared to todays OS's).
It is a single user OS
that can execute one process at a time. DOS had an application programming interface
to allow user programs to access some hardware in a device independent way,
but only for character based applications.

This allowed applications to display graphical elements
emulated with text characters as these screenshots of
Microsoft word for DOS show:

![MS Word 1]({{root_url}}/assets/word1-example-1.png)

This is Microsoft Word version 1.

![MS Word 2]({{root_url}}/assets/word1-example-2.png)

To use these programs you had to remember key combinations to bring up the menus and
used the cursor keys to navigate around the screen.

If the application required fancy graphics, sounds or networking (or just wanted to allow use of a mouse), then the application had to talk directly to that hardware using device specific drivers.

![MS-DOS App Architecture]({{root_url}}/assets/ms-dos app arch.svg | width=400)

If you changed your sound/network/video card, applications might stop working as they might not have drivers for it.


## Windows

On 20th November 1985 Microsoft launched [Windows version 1.0](https://en.wikipedia.org/wiki/Windows_1.0).

The first version of windows ran on top of MS-DOS and presented a Graphical User Interface.

![Windows 1]({{root_url}}/assets/windows1.png)

Windows 1 introduced the hardware abstraction layer into PC application architecture. Windows 1 included drivers for video cards, a mouse, keyboards, printers and serial communications, and applications were supposed to only invoke The Windows APIs and not talk to the drivers directly.

The windows OS has evolved a great deal over the years and the original windows 1 architecture was still in use as the foundation of windows me release in 2000.

starting in 1993 Microsoft created a purely 32 bit OS with no legacy code from the windows 1 architecture. The kernel created for windows NT is still used as the base for current versions of windows (although it has evolved since 1993).

This is the basic structure of windows today.
User applications talk to a layer in the kernel that abstracts
out all details of the hardware and presents a unified api to user applications.

![Windows Architecture]({{root_url}}/assets/windows kernel arch.svg)


## Linux

In 1991, Linus Torvalds, a student at Helsinki university
wanted an OS where he could play with it's source code and learn about
it's internals. He started using an OS called Minix written by professor Andrew Tanenbaum and documented in
a book which was aimed at students learning operating systems design.
While source code for the Minix
system was available, modification and redistribution were restricted.
This led Linus Torvalds to start writing
his own OS which he called Linux.

The first message about Linux was actually posted to the comp.os.minix newsgroup on
![25 Aug 1991 - First msg about Linux](https://groups.google.com/forum/#!msg/comp.os.minix/dlNtH7RRrGA/SwRavCzVE7gJ)

Linux has a similar architecture to current windows versions. no user application accesses
hardware devices directly not even by talking to device drivers.
User applications talk to a layer in the kernel that abstracts
out all details of the hardware and presents a unified api to user applications.

![Linux Architecture]({{root_url}}/assets/linux kernel arch.svg)


# Windows Subsystem for Linux

So, finally on to the subject of this post.

Microsoft hasn't always been a fan of Linux. Some people have even accused
Microsoft of underhand tactics in the past designed to stop Linux being installed on
PC's that also had Windows installed.

But eventually they have realised that developers seem to like the open source OS and have started supporting it.

### [Windows Subsystem for Linux-August 2, 2016 (Windows 10 Build 1607)](https://en.wikipedia.org/wiki/Windows_10#Redstone_1)
the Windows subsystem for linux was written to allow text mode linux programs to be executed on windows.

"WSL executes unmodified Linux ELF64 binaries by virtualizing a Linux kernel interface on top of the Windows NT kernel"

basically it performs real time translation of Linux syscalls into Windows OS syscalls.



![Windows Subsystem for Linux Architecture]({{root_url}}/assets/Windows-Subsystem-for-Linux-Architecture.svg)


essentially microsoft wrote a linux kernel 'emulator', which allows programs that call into
The Linux kernel user-space API to execute on windows and not know it.

https://blogs.msdn.microsoft.com/wsl/2016/06/08/wsl-system-calls/

https://docs.microsoft.com/en-gb/windows/wsl/release-notes

No graphics calls. Xeyes wont run

but unix has a unique take on windowing systems.

http://wsl-guide.org/en/latest/


## Graphical programs and X-Windows

X-Windows abstracted even more so that cheap workstations could run large applications.

![X-Windows Architecture]({{root_url}}/assets/x-windows arch.svg)


So we can install an X-Server on windows and then we can run graphical programs from the WSL.







## References

![The Halloween Documents-1 Nov 1998](http://www.catb.org/~esr/halloween/)





.

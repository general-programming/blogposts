---
title: Sqbika's Keyboard Hacking Adventure, Episode 1
author: Sqbika
discord: 132136706378956800
date: 2019-07-24
---

## Backstory

It started with a cool summer, er no. It was April, 19th when I ordered the keyboard. It was a Motospeed K87S tenkeyless RGB chinese keyboard. IT was good, it was white aand it was closed source.  
What is the first thing in one's mind? Let's hack it!

## Information gathering

I have embarked on this journey with one goal: Have my own RGB profiles and my own macro layers. It wasn't an easy task as there were 0 information regarding this keyboard.
First and foremost I needed to figure out what engine is this machine running on. Took the keyboard apart and took a closer look at the black square chip. It was a BYK870 microcontroller. Searching on the internet yielded almost nothing, except one gist.
  
[The gist](https://gist.github.com/castleberrysam/755c3abfdc996c1dd1a294c74286f5eb) was my rescue, which meant that someone already atempted this.  
Taking a closer look at the gist's author, he had another gist, which was for removing and deciphering the firmware of an updator. A company released firmware updates for the BYK870, so we had access to a firmware. But how do we get it out?   
Looking at [the unpacker gist](https://gist.github.com/castleberrysam/2510f3e87b3d313a27320f165ef5e1cc), it used a modified [TEA](https://en.wikipedia.org/wiki/Tiny_Encryption_Algorithm) encryption. The K870.exe (thats the updater's name) contained the piece of code to deciper the firmware.  
  
Another thing that castleberrysam (the author or the unpacker and the I/O mapping gist) noticed that the BYK870 is a modified MCU of the Sinowealth SH79F6489, a 8051 ASM based microcontroller.  
GREAT! Now we have almost everything to start doing our own firmware. We have a program that can patch, we know the I/O pins, we have instructions for the MCU, except one thing. The compiler

## Compile error: unknown line: "pls compile already" at line 1

I mentioned that it used a modified TEA right? So yeah. The modification is not that severe but reversing the decryption is a bit harder for me than I thought. I went through every change, tried to change everything, nothing good came out.  
Everything was further complicated by the fact, that the K870.exe contained a firmware which wasn't made for the K87S, but for another (pressumably the Z-Element 77). Fiddling around the patcher I successfully patched my keyboard with the wrong firmware. Now the backlight is gone and my keyboard thinks he has a numpad. Very nice...  
The other complication I have encountered is the fact that when I wiresharked the firmware patcher, the packets sent weren't that particularly interesting, but for some reason, I could not ever replace the same events in Python nor Java.  
So I just decided to modify the firmware -> encrypt it back -> patch the K870.exe -> update the firmware -> let's see what happens.  
Since the USB code is excluded / burnt into the MCU (speculation, as after bricking the keyboard beyond repair, plugging the usb back in during flashing, it flashed back the working firmware), I'm free to do whatever I want.
  
And now we are here, renting a 96 vcore cloud server to bruteforce the hex encryption key.

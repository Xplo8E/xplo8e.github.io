---
title: Why Problem-Based Learning Actually Works
date: 2025-10-20
categories: 
- thinking
tags:


---

Ever watch a tutorial and nod along like you get it, then go to actually build something and just... blank? Yeah, that was me for years, especially with iOS stuff and security tools. Turns out there's a better way: just pick a real problem and figure it out as you go. No theory grind first, just dive in and let the debugging teach you. That's problem-based learning. This post is basically me saying "try it" with some examples of when it saved my ass.

Here's the idea: instead of reading a bunch of theory upfront, you just start with something broken that bugs you. You poke at it, add logs, Google the weird errors, whatever. And because you actually care about fixing this specific thing, stuff sticks way better. Yeah, studies say it helps retention or whatever, but honestly the real reason it works is you're not learning random facts—you're learning the exact thing you need right now.

Like, iOS tweak dev. I read the docs, forgot it all. Then I needed to bypass some detection checks and found Shadow, a tweak that does exactly that. So I just grabbed the code, threw in some logs, watched the console output. No lecture, just following the hooks and seeing how it spoofs system calls. Suddenly all that theory I'd skimmed actually made sense because I was seeing it do stuff. Started making my own tweaks after that. Context beats memorizing any day.

Same deal with Frida. I'd been scripting hooks for years but never really got how it worked under the hood—like the connection stuff, injection tricks, all that. Then apps started hanging when I traced them. Figured it was Frida, so I cloned the repo, added a bunch of prints, recompiled it. Traced through the fruity code for USB connections, the tunnel fallback logic, found that transport errors weren't triggering the usbmux fallback—it was treating them as fatal. Made a PR to fix it, but more importantly I actually understood how Frida's connection logic worked now. When you're forced to dig that deep, you can't really half-ass it.

Just recently Frida broke again. Crash logs pointed at systemhook.dylib from palera1n. No source available, so I reversed it in Binary Ninja—spent like two hours in the disassembly just to figure out what that dylib actually does. Found the source later and yeah, I'd read it right. Issue went away on its own, but now I've got this foothold into iOS internals (Mach-O loading, dynamic linking) that I keep building on. These little wins add up—you start seeing how everything connects.

Why bother with this instead of just learning the basics? Because tech doesn't work in a straight line. It's messy and you need to figure stuff out on the fly. This approach makes you good at that. Plus when your hunch actually pans out and fixes the bug, that confidence sticks. Sure, it takes longer sometimes (hello 2am compile sessions), but the stuff you learn this way transfers everywhere.

Not gonna lie though, it can suck sometimes. You'll spend hours going in circles with no guarantee you'll figure it out. Dead ends, second-guessing yourself, getting way deeper than you planned. With that Shadow code I spent an entire weekend just trying to understand how it works. The dylib reversal felt endless until it clicked. It's inefficient if you're on a deadline. But here's the thing—when it does click, you don't just fix the bug. You understand the whole system now. And all those detours? They taught you how to debug, how to think. For learning on your own time, that's worth way more than a clean tutorial path.

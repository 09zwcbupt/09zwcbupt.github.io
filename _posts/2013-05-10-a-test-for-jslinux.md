---
title: a test for jslinux
author: richard
layout: post
permalink: /2013/05/10/a-test-for-jslinux/
categories:
  - 技术
---
User: root  
Useful links:  
<a title="How does bellard.org/jslinux work?" href="http://www.quora.com/Emulators-computing/How-does-bellard-org-jslinux-work" target="_blank">How does bellard.org/jslinux work?</a>  
<a title="Javascript PC Emulator - Technical Notes" href="http://bellard.org/jslinux/tech.html" target="_blank">Javascript PC Emulator &#8211; Technical Notes</a>  
<!--more-->



Thanks to: **https://github.com/ewiger/jsmodem**  *and*  **http://bellard.org/jslinux/**  
some <a title="useful talks" href="https://groups.google.com/forum/m/?fromgroups#!topic/hackerfellowship/SOs1t2y5HHw" target="_blank">useful talks</a> on this topic  
videos on jslinux/jsmodem:  
part1: <a title="JSModem for JSLinux - Part1" href="http://www.youtube.com/watch?v=MEsmgHrKQYM" target="_blank">Demo</a>  
part2: <a title="JSModem for JSLinux - Part2" href="http://www.youtube.com/watch?v=IyvrYYuV3TI" target="_blank">Brief intro</a>  
part3: <a title="JSModem for JSLinux - Part3" href="http://www.youtube.com/watch?v=KPfYsRX8h00" target="_blank">Loading, New device & IO</a>  
part4: <a title="JSModem for JSLinux - Part4" href="http://www.youtube.com/watch?v=lc9a2wH5p9Y" target="_blank">Modem code overview</a>  
part5: <a title="JSModem for JSLinux - Part5" href="http://www.youtube.com/watch?v=79xLwAXNYB8" target="_blank">Speculation on virtualization</a>

Also some other js based linux emulators:  
<a title="http://bellard.org/jslinux/" href="http://bellard.org/jslinux/" target="_blank">http://bellard.org/jslinux/</a> (the original one)  
<a title="http://www.ubercomp.com/jslm32/src/" href="http://www.ubercomp.com/jslm32/src/" target="_blank">http://www.ubercomp.com/jslm32/src/</a>  
<a title="not a demo, but jslinux on Node.js" href="https://github.com/tlrobinson/node-jslinux" target="_blank">https://github.com/tlrobinson/node-jslinux</a>  
<a title="https://github.com/ewiger/jsmodem" href="https://github.com/ewiger/jsmodem" target="_blank">https://github.com/ewiger/jsmodem</a> (What I used for this page)

From http://yauhen.yakimovich.info/blog/2011/05/18/age-of-web-wonders/

> Building JS emulators of processing units is not new. For instance, <a title="JNSES" href="http://benfirshman.com/projects/jsnes/" target="_blank">JSNES</a> emulates Nintendo gaming console allowing to run ROMs of old games as tetris (by Alexey Pazhitnov), contra, donkey kong, etc. Similar (x86) emulators were also developed in pure Java, e.g. <a title="JPC" href="http://jpc.sourceforge.net/home_home.html" target="_blank">JPC</a>.
> 
> Another remarkable <a title="JS Simulator" href="http://www.visual6502.org/JSSim/index.html" target="_blank">JS simulator</a> of <a title="MOS 6502" href="http://en.wikipedia.org/wiki/MOS_Technology_6502" target="_blank">MOS 6502</a> 8-bit processor (both NES and Terminator’s chip) allows to visualize the computational state of the unit. This time authors have taken their time to actually digitalize the full image of the chip, instead of just approximating the computation results or following available VHDL-like semantics. As the result one can see how program runs inside the “X-rayed” chip.
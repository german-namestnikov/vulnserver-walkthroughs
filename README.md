# vulnserver-walkthroughs

Hi there! Here I will store my exploits and all other stuff for [the Vulnserver Application](http://www.thegreycorner.com/2010/12/introducing-vulnserver.html). 

## Peach Pits
I used [Peach Fuzzer](http://www.peach.tech/resources/peachcommunity/) to discover flaws in the Vulnserver Application. I am still a newbie in fuzzing and, especially, in Peach Fuzzer, but I will publish all my Peach Pits when all other work will be finished.

You can use [this pit](https://github.com/proteansec/fuzzyftp/blob/master/peach/vulnserver.xml) which didn't work for me.

It is very important to create correct Data Models to fuzz this app, because some Vulnserver commands require special chars to crash an application or execute your payload. You can see these chars in my exploits or in Vulnserver source code.

## Exploits
Currently, I have only three exploits to use against Vulnserver:
* exploit_trun.py - simple stack-based buffer overflow in TRUN command that executes payload with JMP ESP instruction.

* exploit_hter.py - similar with exploit_trun.py, but all sent chars will be placed in memory as bytes, not char codes. In two words, sent "AAAA" string means not "\x41\x41\x41\x41", but "\xAA\xAA". Based on HTER command.

* exploit_gmon.py - SEH-based exploit that utilizes buffer overflow in GMON command. SEH may be too hard to understand, moreover, this exploit involves jumpcode, because there is too small memory amount to place shellcode after SEH record.

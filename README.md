# vulnserver-walkthroughs

Hi there! Here I will store my exploits and all other stuff for [the Vulnserver Application](http://www.thegreycorner.com/2010/12/introducing-vulnserver.html). 

## Peach Pits
I used [Peach Fuzzer](http://www.peach.tech/resources/peachcommunity/) to discover flaws in the Vulnserver Application. I am still a newbie in fuzzing and, especially, in Peach Fuzzer, so, my pits definitely shouldn't be viewed as best practices. Also, there are a lot of pits for one application and I think that this is a wrong way. I am going to merge all of them in one pit (to rule them all) in a nearest future.

It is very important to create correct Data Models to fuzz this app, because some Vulnserver commands require special chars to crash an application or execute your payload. You can see these chars in Vulnserver source code.

#### Start Agent
```
peach -a tcp
```

#### Start Fuzzing
```
peach vulnserver_gmon.xml TestGMON
```

## Exploits
Currently, I have these exploits to use against Vulnserver (and seems like that is all):
* **exploit_trun.py** - simple stack-based buffer overflow in TRUN command that executes payload with JMP ESP instruction.

* **exploit_hter.py** - similar with exploit_trun.py, but all sent chars will be placed in memory as bytes, not char codes. In two words, sent "AAAA" string means not "\x41\x41\x41\x41", but "\xAA\xAA". Based on HTER command.

* **exploit_gmon.py** - SEH-based exploit that utilizes buffer overflow in GMON command. SEH may be too hard to understand, moreover, this exploit involves jumpcode, because there is too small memory amount to place shellcode after SEH record.

* **exploit_kstet.py** - demonstrates egghunting concept. There is too small place to store your shellcode, but enough to store egghunter. Egg is placed via execution of different vulnserver commands (in hope that one of them will work as planned and store our egg and shellcode in memory).

* **exploit_gter.py** - yet another example of egghunting technique.

* **exploit_lter.py** - task about bad characters where all bytes after 0x7F are forbidden for input.  
 

---
title: Super16, a silly ISA
date: 2021-05-13
---
# Super16... What is it?
Super16 is my custom architecture for a theoretical CPU. It's on [github](https://github.com/l3gacyb3ta/super16)! 
I have designed the thing from the ground up, so here's an overview:  
## Features:
* Text-out support
* 7 16-bit registers
* Binary compilation
* 16-bit data on every instruction
* Built-in screen drawing (pixel by pixel)
  
## Missing stuff:
* Any support for memory, I mean who needs that?
  
## Basic design:
One instruction is composed of 32 bits, making up 3 catagories; Opcode, Register and data. 
The opcode is two hexadecimal digits, the register is another two, and the data is a 4-digit
hexadecimal numbers split into two two-digit numbers.
Here is an example instruction loading ```0xf988``` into ```r5```:  

| Opcode | Register | Data 1 | Data 2 |
|--------|----------|--------|--------|
| 0x20   | 0x05     | 0xf9   | 0x88   |

There are a _ton_ of opcodes/instructions, (but not as may as x86) 19 to be precise.
Here's a table of all the current instructions:

| Opcode | Instruction |                                                                             |
|--------|-------------|-----------------------------------------------------------------------------|
| 0x10   | store       | store reg reg2                                                              |
|        |             | Copy value from one reg to another                                          |
| 0x20   | load        | load reg val                                                                |
|        |             | Load a value into a reg                                                     |
| 0x30   | add         | add reg val                                                                 |
|        |             | Add value to reg                                                            |
| 0x31   | addr        | addr reg reg2                                                               |
|        |             | Adds reg2 to reg                                                            |
| 0x40   | sub         | sub reg val                                                                 |
|        |             | Subtracts val from reg                                                      |
| 0x41   | subr        | subr reg reg2                                                               |
|        |             | Subtracts reg2 from reg                                                     |
| 0x50   | mul         | mul reg val                                                                 |
|        |             | Multipy register by value                                                   |
| 0x51   | mulr        | mul reg reg2                                                                |
|        |             | Multiply reg by reg 2                                                       |
| 0x60   | div         | div reg val                                                                 |
|        |             | Intiger divides the register by the value                                   |
| 0x61   | divr        | div reg reg2                                                                |
|        |             | Initger devides reg by rg2                                                  |
| 0xff   | prt         | prt 0x0000 0x0000                                                           |
|        |             | Print ascii value in p0 reg                                                 |
| 0x0f   | scrn        | scrn 0x0000 val                                                             |
|        |             | Set pixel in x8 and y9 regs to the value (0: black) (1: white)              |
| 0xdd   | drw         | drw 0x0000 0x0000                                                           |
|        |             | Draw screen buffer                                                          |
| 0xf0   | cmp         | cmp reg reg2                                                                |
|        |             | Set cm reg to 0x0001 if bigger, 0x0000 if smaller, and 0xffff if their equal|
| 0xb0   | branch      | branch val label                                                            |
|        |             | Branch to loop if cm is val                                                 |
| 0xb1   | nbranch     | nbranch val label                                                           |
|        |             | Branch to loop if cm is not val                                             |
| 0xbb   | jump        | jump 0x0000 label                                                           |
|        |             | Jump to label                                                               |
| 0x00   | noop        | noop 0x000 0x000                                                            |
|        |             | Literally does nothing                                                      |
| 0xfe   | halt        | halt 0x0000 0x0000                                                          |
|        |             | Halts the cpu                                                               |

As you can see, I've spent _way_ to much time on this.
## Implementing it:
As I have not yet learned how to build an actual sim in logisim or similar software (so many sim-s!), I have implemented this ISA in python.
After running ```assembler.py``` with a valid asembly file as an argument,
a pickle file named rom.pic will appear.
In order to run it, simply execute ```cpu.py``` for normal use, and ```slowpu.py``` for debugging.  
This will give you an accurate emulation of the cpu using any assembly you want.
## Example programs:
```
# Do some math:

load r1 0x0002
load r2 0x0002
mulr r1 r2
```
This is a simple little program that, 1st, loads 2 into ```r1``` and ```r2```, and 2nd, multiplies ```r1``` by ```r2```.
As you know, there are more interesting things you can do with programming. So here we gooooo!  
  
```
# setup r2 and r2
load r2 0x0005
load r1 0x0001
# setup h
load p1 0x0068
.top
# Print h
prt 0x0000 0x0000
# Increment r1
add r1 0x0001
# compare and branch
cmp r1 r2
nbranch 0x0001 top
#
# if it's done, write an g
load p1 0x0067
prt 0x0000 0x0000
```
Wow, that's a lot longer. This bit of code does something really fun.

1. It sets up ```r1```, ```r2```, and ```p0``` with the right values.
  ```p0``` is the special register that saves an ascii code and prints it on a ```prt```
  instruction.
2. We define a label ```.top```, this'll come in help latter! We also print a h for debugging.
3. We then increment ```r1``` by 1. 
4. Fun stuff now! We then compare ```r1``` and ```r2```. If ```r1``` is bigger
  than ```r2```, then ```cm``` will be ```0x0001```.  
  If that's _not_ true, then we'll jump back to ```.top```, other wise we'll print a g.
  
The output then looks like this:  
```hhhhhg```  
So it worked! Magical branches are cool.
## Binaries:
The last feature I'm going to talk about is the building into a binary thing.
Here's the hex representation of the binary for the math program:
```
20 01 00 02
20 02 00 02
51 01 00 02
```
There we go! We can se the ```20``` on the beginging of every line.
That is the opcode for ```load```, and then we see the 2 register names, ```r1``` and ```r2```.  
The last line starts with ```51``` which is the opcode for ```mulr```, and then has the numbers for ```r1``` and ```r2```.
So we can see that it would work on a theoretical CPU!  
  
Thanks for reading,  
  
\- L3gacy 
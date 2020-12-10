
# 1 - Fundamentals of System Hardware

Created: 8 December 2020
Modified: 10 December 2020

## Key Topics

- Definition of a computer
- Types of computers
- What's inside a computer (macro view)
- What each components does
- How components communicate
- How the CPU works
- The memory hierarchy
- Hard disks

## Definition of a computer

The computer is an ***electromechanical*** device which takes input, does processing and produces output.

## Types of computers

- Laptops
- Desktops
- Servers
- Mainframe
- etc.

## Inside a computer

- **CPU** - "brain" of the computer; do all the calculations; includes registers, the CU and ALU, L1 and L2 caches.
- **Main memory** - where codes and data are stored temporarily 
- **Video card / GPU** - stores info to display on the screen; do complex calcuations related to decimal numbers
- **Secondary storage** - Hard drive or Solid state; permanent storage
- **Tertiary storage** - e.g. CD-Rom, DVD, Blu-Ray. Offline storage.
- **Power supply** - provide 5V or 12V DC supply
- **Mainboard / Motherboard** - provides physical connectivity for all the devices, included the system bus and all peripheral busses.

## What's Common?

***All*** computers have

- At least one **Central Processing Unit (CPU)** which is the "brain" of the computer
- **Main memory (RAM)** where codes and data are stored temporarily 
- **Secodary storage** where informatin is stored permanently

***Most*** computers will have

- A **video graphic controller** where images can be rendered for display on a screen
	- GPU - performs efficient ***floating-point arithmetic*** opertions 
- A **network interface** for communications, e.g. Ethernet, FDDI
- **Peripheral interfaces**, e.g. USB, Thunderbolt, Firewire, SCSI

## Communications between the devices

- Internal communications in a machine is done via a **bus**.
- A bus is a **physical pathway** for communcation between two or more devices
- The **system bus** is the main pathway between the CPU and main memory, but also carries data to and from Input and Output (IO) devices.
- USB - universal serial bus

## The CPU

- Designed by computer engineers
- the "brain" of the computer
- a single piece of silicon in the form of chip
	- transistors
	- logic gates
- the only where code is actually executed in the system
- only runs **machine language** code
- operates on a **fetch-decode-execute** cycle
	- fetch an instruction from main memory
	- decode the instruction
	- execute the instruction
- each types of CPU has its own set of **instructions** which is understands
- has a small amount of memory, call **registers** which it uses to perform operations and store results - no latency
- have a **cache** memory to perform more quickly.


## Machine Language

Computers can only understand very basic commands, e.g.

- Move
- Add
- Subtract
- Multiply
- Compare
- Jump
- etc.

Designers of CPUs put the capability to perform these operations in the physical chip.

## Instruction Set

The designers of the CPU create a set of instructions that the CPU can perform.

When the CPU receives a particular instruction, it performs that tasks.

This set of instructions, usually as amll as 100, can each be represented by a numeric value, i.e. the OpCode.

<table align="center">
<thead><tr><th>Instruction</th><th>OpCode</th></tr></thead><tbody><tr><td>ADD</td><td>0x00</td></tr><tr><td>AND</td><td>0x20</td></tr><tr><td>CMP</td><td>0x38</td></tr><tr><td>INT</td><td>0xCD</td></tr><tr><td>JMP</td><td>0xE9</td></tr></tbody>
</table>

## Fetch-Execute Cycle

- The CPU performs a fetch to *move the instruction from main memory into the CPU* (specifically into an instruction register).
- It then decodes the instruction, also moving in any additional data that might be necessary with that instruction.
- It then executes that instruction
- This process repeats with the next instruction in the sequence

## Memory

<p align="center">
	<img src="https://i.imgur.com/lc13yVJ.png" width="50%">
</p>

- The instruction, and all the data, has to come from somewhere.
- In order for code to be executed, it has to be in a register built into the CPU
- Why not just store everything in registers?
	- They are **expensive**



## The Memory Hierarchy

<table align="center">
<thead>
  <tr>
    <th></th>
    <th>Component</th>
    <th>Size (for example)</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Faster and smaller capacity</td>
    <td>Register</td>
    <td>576 B</td>
  </tr>
  <tr>
    <td></td>
    <td>Cache (L1)</td>
    <td>64 KB</td>
  </tr>
  <tr>
    <td></td>
    <td>Cache (L2)</td>
    <td>20 MB</td>
  </tr>
  <tr>
    <td>Slower and bigger capacity</td>
    <td>DDR / Main Memery</td>
    <td>384 GB</td>
  </tr>
</tbody>
</table>


## RAM

- Known as **Random** Access Memory 
- constant access time to any point in the RAM
- Memory are broken ddown into **bytes**, with each byte being able to be accessed independently of the others
- When the computer is turned off, everything in RAM is lost
	- Sleep mode
	- Hibernate mode
- When running a program, all the machine language instructions are brought into RAM and, one-by-one, pull into the CPU by the fetch and execute cycle

## Secondary Storage

Hard Disk Drive (HHD)

- also known as "spinning" drives
- Contain mulitple magnetic material discs which rotate together at a constant velocity
- Contain read heads which move to different radii on the disk
- Allow the system to access any position via it's three dimensional polar coordinates
- Accessing first the innermost radius then the outermost radius takes significantly longer than two adjacent radii.
- Size is usually measured in terabytes.


Solid State Disks (SSD)

- Contain a number of chips like USB flash drives
- Data is stored, electrically, in these chips
- All data can be accessed in the same amount of time
- Due to cost, these drives are smaller than HDDs but perform much faster.


# Reference

- Computer Hardware and Operating Systems
[Daniel Katz-Braunschweig](https://www.edx.org/bio/daniel-katz-braunschweig), Senior Lecturer at Tandon School of Engineering
[Aspen Olmsted](https://www.edx.org/bio/aspen-olmsted), Adjunct Professor at Tandon School of Engineering
New York University
URL: https://www.edx.org/course/computer-hardware-and-operating-systems

---

> Written with [StackEdit](https://stackedit.io/).

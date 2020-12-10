
# 2 - Introduction to Operating Systems

Created: 10 December 2020
Modified: 10 December 2020

## Key Topics

- What is an operating system
- Basics of how operating systems work
- A short history of operating systems
- Preemptive processing concepts
- Architecture of an OS
- Some modern operating systems

## What is an OS?

A program that **controls execution of application programs** and acts as an **interface** between applications and computer hardware.
- A software which manages "the system"
- Runs on the same processor as the user's program code
- Does not include applications

## Layers of Interaction

User <--> Application <--> Operating System <--> Hardware

#### Example

When an application calls `open("file.txt", "r")`, the OS performs a list of operations, incl.

- provides file handle
- determines file location
- accesses file
- marks as read-only



## The Kernel

- The core component of the OS
- Responsible for managing system sources
	- Memory management - RAM
	- Process scheduling - CPU time
- Assists applications with performing work

## Back in the Olden Days

When mainframes dominated the computing industry:

- The computer ran only **one** program at a time
- The one program had complete access to all the system resources
- The OS was only responsible for getting programs ready to run
- Requires JCL: job control language
- The mainframe operator (a human) decided which order to run programs in
- When one program finished, the OS was ready with the next that wanted to run
- This is called batch multiprogramming

## Today's Environment

- Today, we have lots of processing power and lots of resources - enough to run multiple programs at the same time
- The OS becomes a resource manager
	- The OS manages allocation of resources, incl. memory, CPU time, file handle, network connection
	- The OS decides which programs can run and when
	- The OS will stop and restart running programs, preemption
	- This is called time sharing

## OS Levels

<table align="center">
<thead>
  <tr>
    <th></th>
    <th>Level</th>
    <th>Name</th>
    <th>Brief Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="6">Other OS</td>
    <td>13</td>
    <td>Shell</td>
    <td>user interfaces</td>
  </tr>
  <tr>
    <td>12</td>
    <td>User Processes</td>
    <td></td>
  </tr>
  <tr>
    <td>11</td>
    <td>Directories</td>
    <td></td>
  </tr>
  <tr>
    <td>10</td>
    <td>Devices</td>
    <td></td>
  </tr>
  <tr>
    <td>9</td>
    <td>File Systems</td>
    <td></td>
  </tr>
  <tr>
    <td>8</td>
    <td>Communications</td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="3">Kernel</td>
    <td>7</td>
    <td>Virtual Memory</td>
    <td></td>
  </tr>
  <tr>
    <td>6</td>
    <td>Secondary Storage</td>
    <td></td>
  </tr>
  <tr>
    <td>5</td>
    <td>Primitive Processes</td>
    <td>e.g. system scheduling</td>
  </tr>
  <tr>
    <td rowspan="4">Hardware</td>
    <td>4</td>
    <td>Interrupts</td>
    <td></td>
  </tr>
  <tr>
    <td>3</td>
    <td>Procedures</td>
    <td></td>
  </tr>
  <tr>
    <td>2</td>
    <td>Processor Instruction Set</td>
    <td>i.e. the processor architecture</td>
  </tr>
  <tr>
    <td>1</td>
    <td>Electronic Circuits</td>
    <td></td>
  </tr>
</tbody>
</table>

## The Windows Model

<p align="center">
	<img src="https://i.imgur.com/9Y7XPxV.png" width="50%">
</p>

> source: https://www.edx.org/course/computer-hardware-and-operating-systems

## The HAL

- HAL - Hardware Abstraction Layer
- Different types of systems have slightly different hardware
- a layer which can provide the kernel with a set of functions to call which program the hardware properly
- Changes to hardware only require chanding the HAL, not rewriting the whole OS

## Windows Device Drivers

- Device drivers are kernel-layer software written by companies that design hardware
- They provide functions for the kernel to call in order to access the hardware
- They were the cause of frequent "blue screening" before Windows Hardware Quality Labs (WHQL)


## UNIX

- A multi-user, multi-tasking OS
- started by AT&T Bell Laboratories
- Designed to allow users to manage their own tasks
- Released into public domain as open source software
- Comes in many different flavors: AIX, Linux, Solaris, etc.
- Has been modified many, many times


# Reference

- Computer Hardware and Operating Systems
[Daniel Katz-Braunschweig](https://www.edx.org/bio/daniel-katz-braunschweig), Senior Lecturer at Tandon School of Engineering
[Aspen Olmsted](https://www.edx.org/bio/aspen-olmsted), Adjunct Professor at Tandon School of Engineering
New York University
URL: https://www.edx.org/course/computer-hardware-and-operating-systems

---

> Written with [StackEdit](https://stackedit.io/).

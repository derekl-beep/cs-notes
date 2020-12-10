
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


# Reference

- Computer Hardware and Operating Systems
[Daniel Katz-Braunschweig](https://www.edx.org/bio/daniel-katz-braunschweig), Senior Lecturer at Tandon School of Engineering
[Aspen Olmsted](https://www.edx.org/bio/aspen-olmsted), Adjunct Professor at Tandon School of Engineering
New York University
URL: https://www.edx.org/course/computer-hardware-and-operating-systems

---

> Written with [StackEdit](https://stackedit.io/).

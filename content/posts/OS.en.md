---
title: "OS"
date: 2019-12-13T22:27:52-08:00
draft: false
---
<!--more-->

An operating System is a program that manages the computer hardware.

It also provides a basis for Application Programs and acts as an internediary between computer User and computer Hardware.

Functions of OS:

* It is a interface between Use & Hardware
* Allocation of Resources
* Management of Memory, Security, etc.

## Structure of Operation System

A modern general-purpose computer system consists of one or more CPUs and a number of device controllers connected through a common bus that provides access to shared memory.

* Each device controller is in charge of a specific type of device
* The CPU and the device controllers can execute concurrently, competing for memory cycles.
* To ensure orderly access to the shared memory, a memory controller is provided whose function is to synchronize access to the memory.

Some inportant terms:

* Bootstrap Program:
  * The initial program that runs when a computer is powered up or rebooted.
  * It is stored in the ROM
  * It must know how to load the OS and start executing that system
  * It must locate and load into memory the OS Kernel
* Interrupt:
  * The occurence of an event is usually signalled by an interrupt from hardware and software
  * Hardware may trigger an interrupt at any time by sending a signal to the CPU, usually by the way of the system bus.
  * When the CPU is interrupted, it stops what it is doing and immediately transfers execution to a fixed location.
    * The fixed location usually contains the starting address where the Service Routine of the interrupt is located.
    * The Interrupt Service Routine Executes.
    * On completion, the CPU resumes the interrupted computation.
* System Call:
  * Software may trigger an interrupt by executing a special operation called System Call.

## Storage Structure

* Registers
* Cache
* Main Memory （RAM）
  * Everything that executes in computer should load to main memory first
* Electronic Disk
* Magnetic Disk
* Optical Disk

**Volatile**: Loses its contents when power is removed.

* Registers, Cache, Main Memory

**Non Volatile**: Retains its contents even when power is removed.

* Electronic Disk

## I/O Structure

* Storage is only one of many types of I/O devices within a computer

* A large portion of operating system code is dedicated to managing I/O, both because of its importance to the reliability and performance of a system and because of the varying nature of the devices.
* A general-purpose computer system consists of CPUs and multiple device controllers that are connected through a common bus.
* Each device controller maintains **Local Buffer Storage** and **Set of Special Purpose Registers**
* Typically, operating systems have a device driver for each device controller
*  This device driver understands the device controller and presents a uniform interface to the device to the rest of operating system.

**Working of an I/O Operation**:

## Computer System Architecture

Types of Computer System based on number of General Purpose Processors:

* Single Processor Systems
  * One main CPU capable of executing a general purpose instruction set including instructions from user processor.
  * Other special purpose processors are also present which perform device specific tasks.
* Multiprocessor Systems
* Clustered Systems








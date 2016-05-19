---
type: homepage
title: "Spinal user guide"
tags: [user guide]
keywords: spinal, user guide
last_updated: Apr 19, 2016
sidebar: spinal_sidebar
toc: false
permalink: /
---

## Document purpose and structure
This site presents the *Spinal* language and how to use it on concrete examples. This documentation also explains how the language is implemented. The documentation is split into different sections:

1. [Languages principles](/SpinalDoc/) (this document)
1. [Getting started](/SpinalDoc/spinal_getting_started)
1. [Language principles and primitives](/SpinalDoc/spinal/core/introduction.md)

## What is Spinal ?
Spinal is a high-level hardware description language. It can be used as an alternative to VHDL or Verilog and has several advantages over those.

{% include note.html content="Spinal is *fully interoperable* with standard VHDL-based EDA tools (simulators and synthetizers) as the output generated by the toolchain is VHDL. <br/><br/>It also enables mixed designs where Spinal components interoperate with VHDL or Verilog IPs." %}

### Advantages of using Spinal over VHDL / Verilog
As Spinal is based on a high-level language, it provides several advantages to improve your hardware coding:

1. *No more endless wiring* - Create and connect complex buses like AXI in one single line.
1. *Evolving capabilities* - Create your own buses definition and abstraction layer.
1. *Reduce code size* - by a high factor, especially for wiring. This enables you to have a better overview of your code base, increase your productivity and create fewer headaches.
1. *Free and user friendly IDE* - Thanks to scala world for auto-completion, error highlight, navigation shortcut and many others.
1. *Detailed information about your design* - Directly extract information from your digital design and generate reports that contain information about latency and addresses.
1. *Powerful and easy type conversions* - Bidirectional translation between any data type and bits. Useful to load a complex data structure from a CPU interface.
1. *Loop detection* - Tools check for you that there is no combinatorial loop / latch.
1. *Clock domains safety* - The tools inform you that there is no user unintentional cross clock domain.
1. *Generic design* - There are no restrictions to the genericity of your hardware description by using Scala constructs.

### What are the differences between Chisel VS Spinal ?
It is a very good question ! Why develop a new language when there Chisel has been released 3 years ago ?

[Chisel](https://chisel.eecs.berkeley.edu/) is the project at the origin of Spinal and Chisel it represents a big step forward compared to common HDL. However, it has several drawbacks for large designs that mix multiple clock domain and external IP (black-boxes). In fact, Chisel show some serious conception issue :

#### Multiple clock support is awkward:

- Working into a single block with multiple clock is difficult, you can't define "ClockingArea", only creating a module allow it.
- Reset wire is not really integrated into the clock domain notion, sub module loose reset of parent, which is really annoying.
- No support of falling edge clock or active low reset.
- No support for asynchronous reset
- No clock enable support.
- Chisel makes the assumption that every clock wire come from the top level inputs, you don't have access to clock signal.

#### Syntax could be better:
- Not pretty literal value syntax, No implicit conversion between Scala and Chisel types.
- Not pretty input/output definition.
- Switch statement doesn't have default case.
- No "Area" notion to give a better structure to the user code.
- No enumeration support

#### Various issue :
- Assignment operator is only checked when you generate the code, the IDE can't check it for you. Bundle assignment operator is weak typed.
- Can't add attribute into generated verilog
- You can't define function without argument into `Bundles`.
- There is no notion of "Area".
- Using `when`/`otherwise` is not strict in all case. This allows you to generate an asynchronous signal that is not assigned in every case.
- You can't write a given range of bit into a bit vector (UInt,SInt,Bits).
- The library that is integrated into Chisel and that provides you some utils and useful bus definition is a good intention, but could be so better and more complete
- When an assignment occur, bits width is automatically resized to match. It should at least generate a warning or an error.
- No cross clock domain checking
- No verilog attribute specification possibilities.
- Unreadable generated code
- They are now moving to FIRRTL (Chisel 3.0) which remove the possibility to analyse the netlist (latency, delay, connections) during the scala generation phase.

For some major issues mentioned here, an issue/pull request was open on github, without effect. In addition, if we consider the age (4 years at the time of writing) of Chisel, this is a very serious issue and it's why SpinalHDL was created.

## Getting started
Want to try it for yourself? Then jump to the [getting started section](/SpinalDoc/spinal_getting_started) and have fun!
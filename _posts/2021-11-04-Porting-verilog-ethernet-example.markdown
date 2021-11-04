---
layout: post
title:  "Porting verilog-ethernet example to a new platform"
date:   2021-11-04 11:00:00 -0400
categories: FPGA documentation ethernet GF-MINUS1
---
## Introduction
This week, I've been porting the verilog-ethernet example design to the GF-MINUS1 platform.
Current Gluten boards use an Ethernet/MII interface between the FPGA and the MCU as the main
communication bus. I've used both the Versa design which I had previously ported and the
ML605 which uses the GMII interface instead of the RGMII. Unlike those design, GF-MINUS1
only supports up to 100Mb interface, but at the time of this writing, it has not been
simulated nor tested on a board.

## Toolchain
Verilog-ethernet uses plain Makefiles to build the example design and optionally flash it to the FPGA.
The main effort was to adapt the templates to use the Yosys/nextpnr-ice40/icestorm instead of Xilinx ISE.
This had started with the ECP5 port, but nextpnr required more attention for arch specific flags (pcf vs lpf).

## Constraints
Constraints were previously located at the top level directory of the example design. I've decided to
move them to the pcf directory since nextpnr splits the pin constrains and the timing constrains.

## Arch dependant blocks (IOs/PLLs/RAM/DSP)
I was ready to migrate some of the arch specific code, but my first build generated no errors on the generic
code in the IP. I'll need to test it on the board to evaluate the functionality or at least get simulation going.

## Interface (MII/RGMII/10G)
The IP implements various interfaces and it is important to select the right one based on
what the board supports. Since I based the design on the Versa port, I had to migrate the
RGMII interface to the GMII interface. I used the ML605 as a reference.

## Testbenches (WIP)
I have yet to try the testbenches, but will update once working

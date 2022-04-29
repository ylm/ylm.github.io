---
layout: post
title:  "Phase Locked Loop"
date:   2022-03-02 19:40:44 -0400
categories: PLL FPGA beginer
---

# Introduction

One important aspect of using a Phase Locked Loop (PLL) in an FPGA is making sure the PLL is properly initialized before the output clock can be used.

# The issue

When coming out of reset, the PLL output signal is unstable. The output is fedback in a control loop which takes time stabilize. The output signal takes a few cycles before oscillating starting at lower frequencies, then ramping up to overshoot the target frequency to finally settle to the target frequency.
While the behaviour of the output signal can be analyzed with negative feedback control theory, the analysis is out of scope of the current article.

# The implications

Considering the unstability of the output signal, it is likely that the timing constrains of the dependant logic will be violated. This might lead to metastability, a faulty output of the register, causing possible malfunctions.

# The solution

The proper way to prevent logic from reaching a faulty state is to hold the downstream logic in reset until the PLL is locked. That will prevent registers from changing state while their input might be changing.

Thanks for stopping by!
Come see me on my [Twitch channel][twitch-channel]!

[twitch-channel]: https://twitch.tv/gatin00b

---
layout: post
title:  "Signal resampling on FPGA: Distributed Arithmetic"
date:   2021-08-16 19:40:44 -0400
categories: DSP FPGA Interpolation audio
---
# Introduction

In the last article, we reviewed important concept of resampling. In this article, we are going to have a look on how the interpolation was implemented.

# Distributed Arithmetic

Considering I might target an FPGA without hard IP multipliers (commonly named DSP slices), I thought it would be wise to implement the filter using a multiplierless architecture. A quick search lead me to the Distributed Arithmetic architecture.

## Theory

From this [article][DA-ref], distributed arithmetic "is an interesting method of efficiently implementing multiply-and-accumulate operations."
Further, "it should be noted that the DA method is applicable only to cases where the multiply-and-accumulate operation involves fixed coefficients."

In distributed arithmetic, the result of a multiply-and-accumulate (MAC) operation is computed serially by accumulating the pre-added values of the coefficients and shifting the result effectively dividing by two. The signedness is handled by substracting the pre-computed values for the most significant bit (signedness bit).

## Implementation

The ice40 architecture uses LUT4 as basic elements. Unlike most FPGAs, the carry chain is placed in front of the LUT. This is important as it requires an additional cell per bit to compute the 2's complement for substractions. As we are close to the timing performances of the FPGA, I wanted to make sure we used as few levels of logic as possible. At most two levels of logic would need to be used.
At most two non-zero samples will be "live" in the filter at the same time. This saves logic resources as we can take out the zero operands.
Because we are interpolating at a ratio higher than the numbers of bits per sample, we can interpolate the samples completely before a new sample comes in.
Since every interpolated sample uses the same original samples but with different coefficients, we take advantage of the parallelism of FPGAs by computing samples in parallel for a higher throughput.

# Solutions

For the development of the interpolator, I've designed a few scripts to help me out.

## interpolator.py

This script generate the filter coefficients. It implements both a Kaiser window function and a sinc function for that purpose.

## txt2raw.py
This script is used to convert text into binary data to further be processed by sox with the intent to convert that data to a wav file.

# Conclusion
That wraps up the mini-series on signal interpolation. While the implementation is efficient, it can use a fair amount of resources on smaller FPGAs. A few issues that still need attention is the overflow in the filter computation and the possibility to re-use some of the block to further reduce resource consumption.


Thanks for stopping by!
Come see me on my [Twitch channel][twitch-channel]!

[twitch-channel]: https://twitch.tv/gatin00b
[DA-ref]: https://www.allaboutcircuits.com/technical-articles/introduction-to-distributed-arithmetic/
[sinc-filter]: https://ccrma.stanford.edu/~jos/resample/Implementation.html
[sinc-func]: https://ccrma.stanford.edu/~jos/mdft/Sinc_Function.html


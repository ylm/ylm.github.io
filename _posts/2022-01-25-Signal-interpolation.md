---
layout: post
title:  "Signal Resampling on FPGA: Interpolation"
date:   2022-01-25 19:40:44 -0400
categories: DSP FPGA Interpolation audio
---
# Introduction

While testing various Delta-Sigma modulator implementations, I realized that upsampling the input signal would not be enough.
Interpolation is the process of computing the samples value in a new sampling rate while preserving the original frequency spectrum.
The ideal interpolation filter is the sinc filter, but its implementation is impractical for our application.

# Resampling: A mix of decimation and interpolation

When talking about resampling, we refers to the process converting a signal from one sampling rate to another sampling rate.
If the new sampling rate is lower than the original one, we talk about decimation and we need to filter the signal prior decimation to avoid frequency aliasing.
If then new sampling rate is higher than the original one, we talk about interpolation. We filter the signal after the interpolation process to remove harmonics.

# Upsampling vs interpolation

Upsampling is usually defined as the act of inserting samples to increase the sampling rate at a certain ratio.
Interpolation is the process of determining the value of those samples while preserving the frequency spectrum of the original signal.

## Zero padding

In the upsampling stage, zero valued samples are inserted instead of holding the sample value. This allows optimization on the filter as we save multiplications.

# Sinc filter

The sinc filter is the ideal interpolation filter. It is the result from an inverse Fourier transform of an ideal low-pass filter.
It is more practical to sample the continuous sinc function than to obtain the coefficients from an inverse Fourier transform.
![sinc funtion](/media/sinc.png)
![sinc frequency reponse](/media/sinc_fft.png)

# Conclusion
Now that we've seen the theory, the next article is going to be about implementation details.

Thanks for stopping by!
Come see me on my [Twitch channel][twitch-channel]!

[twitch-channel]: https://twitch.tv/gatin00b
[DA-ref]: https://www.allaboutcircuits.com/technical-articles/introduction-to-distributed-arithmetic/
[sinc-filter]: https://ccrma.stanford.edu/~jos/resample/Implementation.html
[sinc-func]: https://ccrma.stanford.edu/~jos/mdft/Sinc_Function.html


---
layout: post
title:  "Upsampling vs Resampling"
date:   2022-01-05 20:19:30 -0400
categories: DSP math audio
---
# Introduction

While simulation various Pulse Density Modulators (PDM), I figured I would have to resample the incoming signal as the upsampled signal showed excessive image noise at the ouput of the DAC.

# Upsampling

Upsampling is the process adding samples to a signal to convert from a lower sampling rate to a higher sampling rate. Usually, we insert zero amplitude samples as to not insert additional noise with the added benefit to optimize the interpolation (aka resampling) process. This process creates what is called an image of the frequency content at higher frequencies.
Another way to upsample, in an attempt to resample, is to repeate the previous sample in a sample and hold fashion. This is also incorrect as it also generates harmonics in addition to the image of the frequency without the benefit of the optimized interpolation filter.
![upsampleBad](/media/upsample_bad01.png)
![upsampleFFTBad](/media/upsample_fft_bad01.png)

## Resampling

Resampling also known as interpolation is the process of converting a signal from a sampling rate to another while preserving the original frequency components of the signal. It differs from upsampling or downsampling by the use of a filter to properly remove any harmonic noise from the signal. The ideal interpolation filter is based on the sinc funtion to generate the coefficient of the filter.
![resample](/media/resample_good.png)
![resample fft](/media/resample_fft.png)

# Conclusion

In the next article, we are going to have a proper look at signal interpolation and the sinc filter.

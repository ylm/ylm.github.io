---
layout: post
title:  "Introduction to control theory"
date:   2022-04-29 19:40:44 -0400
categories: introduction
---

# Introduction

Control theory is a set of tools by which we can analyze and design control systems.
Control systems are designed to regulate a system by minimizing the error within a feedback loop to reach a certain command.
The textbook example of a control system is the cruise control of a vehicule.

# Feedback loop

The feedback loop is what characterize the control system. The difference between command (the input) and the output is the error. A control system seeks to minimize that error.
Because of that feedback loop, the stability of the system is not guaranteed.

# Stability

While there are ways to analyze the stability of a system, one thing to keep in mind is the dephasing of the signal. When the output is 180 degrees (pi radians) out of phase with the input, the system will osciallate trying to catch up with itself.

# Conclusion

This was a simple introduction to control theory. In the next article, we are going to dig a bit more into the various transforms we can use to analyze such systems.

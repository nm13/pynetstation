# A longer version of the introduction #

It is about psycho- and neuro- physiology, EGI Netstation, and Python .

Python is **the** language for scientific programming, or at least the #1 candidate for top list . So if you do psychophysiology, it is not unlikely that you may implement some experiment for it using Pygame, Pyglet, VPython, or something more top-level like VisionEgg or PsychoPy .

It is also possible that you may have EGI NetStation system to do EEG recording .

This module allows one to use both things in connection .

Note: I do not claim this is the only Python implementation of such a thing : a module like that may exist within systems like PsychoPy or VisionEgg -- or at least may appear there one day .

I just needed something that does not depend on any big things, something that I am going to test before I use it, so it would be much better if I am well acquainted with it's code. So I wrote it.

I'm sorry if the code internally does not look nice (these were the 3rd and fourth implementations of the module, so I was kinda in a hurry), but we did test it, and in fact, it contains some workarounds for discovered NetStation bugs as well ( I did not feel like they were very willing to quickly solve programming issues, though the contact person was nice, responsive, and, what is very important, tended to provide competent and adequate information about the current problems with the software or documentation ) .

Next: [Features](Features.md)
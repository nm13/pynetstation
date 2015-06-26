A Python module to communicate with EGI NetStation, similar to C++ [libnetstation](http://code.google.com/p/libnetstation/) library ( if that project will go down, see [www.andrewbutcher.net](http://www.andrewbutcher.net/) ) .

As it is easier (for the price of writing less-efficient code) to do things in Python, we have full attribute support and two versions of the implementation -- one for simple "synchronous" communication -- and an "asynchronous" version that does all the communication in a separate thread .

The first one is good for tests, and after setting up things one has to change only three lines to switch to a "threaded" ("asynchronous") version.

[More ... ](ShortDescription.md)

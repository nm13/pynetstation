# Intro #

A Python module to communicate with EGI NetStation, similar to C++ [libnetstation](http://code.google.com/p/libnetstation/) library .

As it is easier (for the price of writing less-efficient code) to do things in Python than, say, in C++, we have full attribute support and two versions of the implementation -- one for simple "synchronous" communication -- and an "asynchronous" version that does all the communication in a separate thread .

The first one is good for tests, and after setting up things one has to change only three lines to switch to a "threaded" ("asynchronous") version.


# Details #

Actually, this is just a small module with some documentation, examples and screenshots: )

Experienced (and impatient) Python programmers may want to go to the [download](Installation.md) section -- and then may be take a look at the [examples](Examples.md).

And for the rest, especially for those whose native language is not Python, there are some more pages that may (or may not) be useful :

  * [Introduction](LongerIntroduction.md)
  * [Features](Features.md)
  * [Installation/Download](Installation.md)
  * [Examples](Examples.md)
  * [Screenshots](ExampleIllustrated.md)
  * [Reference](Reference.md)
  * [Technical Details]
  * [Bugs or Netstation related issues](Bugs.md)
  * [Contacts](Contact.md)

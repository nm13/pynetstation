# Features #

There are two good things -- and some additional details.

Two good things are:
  * we can send the marker with any simple Python data attached : integers, strings and floating-point values ;
  * we have tested it -- i.e. there is there is a workaround for [an evil buffer underflow](http://code.google.com/p/libnetstation/source/detail?r=6) bug that seems to live in the NetStation code .

The additional details -- we have _two_ implementations of the communication component : one simple to be run in the same thread as the main application -- especially useful for debugging -- and one a little bit more sophisticated that spawns an additional "delivery" thread that does the actual communication -- so that the main thread won't be blocked/delayed for communication with Netstation. In some experiments even small delays of millisecond order are important.

In the case of necessity the later implementation could be turned into one that uses different processes instead of threads by utilizing the Python multiprocessing module.

Next: [Installation](Installation.md)
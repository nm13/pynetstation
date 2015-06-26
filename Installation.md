

# Python version #

The code was mostly tested under Python 2.6, though Python 2.5 probably also wouldn't be a problem (but I don't promise).

One could probably use the [2to3](http://docs.python.org/library/2to3.html) script to convert the code for Python 3000, as both the "simple" and "threaded" versions of the code are mostly plain Python without any weird tricks.


# Installation #

Installation is done in simplistic way:
[download](http://pynetstation.googlecode.com/files/egi_20100719.zip), [unzip](http://www.7-zip.org/) and move the "egi" folder into your project directory; after that, the instruction
```

import egi.simple as egi
```
should run silently (I assume you start python interpreter session in your project folder and enter this command, or do sth equivalent).

Otherwise, if you get an ImportError message like the one below
```

Traceback (most recent call last):
File "<stdin>", line 1, in <module>
ImportError: No module named egi.simple
```
then the "egi" folder is probably not in the Python module search path, and You may want to take a look at [this page about python modules](http://www.tutorialspoint.com/python/python_modules.htm) or [standard Python documentation](http://docs.python.org/tutorial/modules.html) to see why .

# Examples #

You may now want to go to the [Examples](Examples.md) section or [directly download the examples code](http://pynetstation.googlecode.com/files/examples_20100719.zip), put it in the folder that contains the "egi" one, and try them yourself.



Next: [Examples](Examples.md)
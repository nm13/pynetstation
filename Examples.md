

# Usage examples #

Here are two almost identical files:
  * one, heavily commented, that shows the use of the ["threaded" version](https://code.google.com/p/pynetstation/source/browse/example_multi.py) of the component ([html version](http://wiki.pynetstation.googlecode.com/hg/html/example_simple.py.html))
  * and another, not so heavily commented, that show the use of the ["simple" version](https://code.google.com/p/pynetstation/source/browse/example_simple.py) of the component ([html version](http://wiki.pynetstation.googlecode.com/hg/html/example_multi.py.html))
.

Either of those can be used, the almost only syntactical difference (I mean, strip all the comments and see what has left) between the two is the first _import_ line:
| `import egi.threaded as egi` | **vs** | `import egi.simple as egi` |
|:-----------------------------|:-------|:---------------------------|


( Ok, there are also different _words_ intentionally used for initialization and deinitialization,

| **"simple" version**    | **"threaded" version**  |
|:------------------------|:------------------------|
| `connect()`             | `initialize()`          |
| `diconnect()`           | `finalize()`            |


but that's really all. )



# Example code distilled #

This is the best I managed to get "in five minutes" using the `<code>` tag; of course in the actual code all the lines start from the same position -- from the beginning of the line ("zero offset").

```


# >>> import and initialization >>>

import egi.simple as egi
## import egi.threaded as egi

# ms_localtime = egi.egi_internal.ms_localtime
ms_localtime = egi.ms_localtime


ns = egi.Netstation()
ns.connect('11.0.0.42', 55513) # sample address and port -- change according to your network settings
## ns.initialize('11.0.0.42', 55513)
ns.BeginSession()

ns.sync()

ns.StartRecording()



# >>> send many events here >>>

## # optionally can perform additional synchronization
## ns.sync()
ns.send_event( 'evt_', label="event", timestamp=egi.ms_localtime(), table = {'fld1' : 123, 'fld2' : "abc", 'fld3' : 0.042} )



# >>> we have sent all we wanted, time to go home >>>

ns.StopRecording()

ns.EndSession()
ns.disconnect()

## ns.EndSession()
## ns.finalize()

# >>> that's it !
```

  * [Here is a link to the same code](https://code.google.com/p/pynetstation/source/browse/example_simple_distilled.py) with standard Google Code formatting style (which I am not still completely happy with) .
  * [Version of colorization](http://wiki.pynetstation.googlecode.com/hg/html/example_simple_distilled.py.html) that uses separate color for the '##' comments (what I prefer personally) .
  * And [here](ExampleIllustrated.md) is the above code illustrated with screenshots -- moved to a separate page as some of the images are moderately heavy .




# Or the same thing split into small parts #

Basically all we do is:
  * import the module :
```
 import egi.simple as egi ```
  * create the "communicator" object and initialize it:
```

ns = egi.Netstation()
ns.connect('address', port)
ns.BeginSession()
```
  * syncronize the clock on Netstation machine with our local system:
```
 ns.sync() ```
  * **now really do send something :**
```

ns.send_event( 'evt_', label="event", timestamp=egi.ms_localtime(), table = {'fld1' : 123, 'fld2' : "abc", 'fld3' : 0.042} )
```
  * close the connection :
```

ns.EndSession()
ns.disconnect()
```

The remaining commands are actually code equivalents of what the user can manually do with the Netstation:
|```
ns.StartRecording()```| Click the "Record" button |
|:-------------------------|:--------------------------|
|```
ns.StopRecording()``` | Click the "Stop" button   |


# The send\_event() command #

The only a little bit tricky command is the `send_event()` thing.

There are three things to be commented, all related to time synchronization issues :

  1. in general it is a good idea to call sync() as often as possible ([libnetstation](http://code.google.com/p/libnetstation/) usage example implies that synchronization happens on every presentation of the stimulus ) ;
  1. it is important to explicitly use the _timestamp_ argument, feeding it with a value provided by the _egi.ms\_localtime()_ call : if the argument is omitted, the "threaded" version asks for the timestamp **on the actual moment of delivery** of the event, that may happen a few milliseconds later.
  1. as the EGI Experimental Control Protocol specifies the internal timestamp as a 32-bit value, the egi.ms\_localtime() call truncates the current timestamp into some value "modulo one billion" -- i.e., we send only the last 9 digits of the actual timestamp ; in other words, approximately every 10 days this may cause a significant shift in the marker timestamps recorded by NetStation, equal approximately 1.000.000.000 milliseconds. If NetStation won't show it's default reaction (crash), such a jump will be probably very easy to detect in almost any recording )

(I have added some workaround for this unlikely situation and am going to upload it shortly after some basic testing. )


Ok, one additional side note is the reminder about the thing from the NetStation docs: according to EGI manuals ("EGI Systems Technical Manual", etc), **all Netstation ids must consist of exactly four characters** -- both event marker ids, or "tags", and the "field" tags that we pass as the dictionary keys in the **table** argument of the _send\_event()_ function.


# See Also #

  * There would also be some [discussion of technical details](TechnicalDetails.md) -- added later.
  * See also the [Bugs](Bugs.md) section .

Next: [Reference](Reference.md)
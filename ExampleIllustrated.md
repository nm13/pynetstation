Here is again some sample code -- and the corresponding data recorded by NetStation .



# The code #

This is the best I managed to get using the `<code>` tag; of course in the actual code all the lines start from the same position -- from the beginning ))

```


import egi.threaded as egi

import sys # sys.argv[]
import time # time.sleep()

ms_localtime = egi.ms_localtime


#
# Panels / Multi-Port ECI --> log
# or just Panels --> Log (I assume you have selected 'Long Form')
#

ns = egi.Netstation()

# sample address and port -- change according to your network settings
ns.initialize('11.0.0.42', 55513)
# Multi-Port ECI Window: "Connected to PC"

ns.BeginSession()
# log: 'NTEL' \n

ns.sync()
# log window: the timestamp ( the one provided by ms_localtime() )


ns.StartRecording()
# recording starts )

time.sleep(5) # pretend we do sth very useful here ...

ns.send_event('evt1')
# log window: shows event id in single quotes
# ( there are also timestamps -- Netstation local time since the beginning of the session )

time.sleep(0.1)  # for the sake of example --
# -- force the events to arrive in the "correct" order :
# as Netstation re-sorts events according to their timestamp values,
# the events that have the same millisecond for the timestamp value,
# may change their order of appearance in the event list .
# so we introduce some additional short artificial delay
# to help our events look nicely in the log and event list .


ns.send_event('evt2', label="event2")
# log window: label without quotes
time.sleep(0.1)  # force the events to arrive in the "correct" order


ns.send_event('evt3', label="event3", description="this is a description of event 3")
# log window shows the description as well

time.sleep(0.1)  # force the events to arrive in the "correct" order

ns.send_event('evt5', timestamp=egi.ms_localtime())
ns.send_event('evt6', description='back in time', timestamp=egi.ms_localtime() - 50)

# Note that in the Log Window the events appear in the order of posting,
# but with "correct" timestamps ( i.e. last has a timestamp that is 50 ms "earlier" than the previous )

time.sleep(0.1)  # force the events to arrive in the "correct" order


#
# two realistic examples
#

ns.send_event( 'evt_', timestamp=egi.ms_localtime() )

ns.send_event( 'evt_', timestamp=egi.ms_localtime(), table = {'fld1' : 123, 'fld2' : "abc", 'fld3' : 0.042} )

# log window: Now we have fields -- they may come in the 'wrong' order
#  ... 1.  'fld2' : abc ,
# but if the event identifiers are unique ( and they *should* be ), this is not important .

time.sleep(0.1)  # force the events to arrive in the "correct" order

ns.send_event('stop') # just to have some "end of session" marker in the log

time.sleep(5) # for symmetry )

ns.StopRecording()
# recording stops )
# NB: in our session default settings we have default timeout equal to 20 seconds.
# if in your case the timeout is shorter -- the recording obviously will stop earlier )

ns.EndSession()
ns.finalize()

```

# The output (screenshots) #

Click on any image to see a full-size picture:

| Screenshot of the desktop with the Multi-Port ECI Log Window | <a href='http://wiki.pynetstation.googlecode.com/hg/img/desktop_log_01.png'><img src='http://wiki.pynetstation.googlecode.com/hg/img/t_desktop_log_01.png' alt='link to the image' title='click to see the full image' /></a> |
|:-------------------------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| The log window itself                                        | <a href='http://wiki.pynetstation.googlecode.com/hg/img/log_window_002.png'><img src='http://wiki.pynetstation.googlecode.com/hg/img/t_log_window_002.png' alt='link to the image' title='click to see the full image' /></a> |
| The event list of the session (reopened after the recording) | <a href='http://wiki.pynetstation.googlecode.com/hg/img/event_list_003.PNG'><img src='http://wiki.pynetstation.googlecode.com/hg/img/t_event_list_003.PNG' alt='link to the image' title='click to see the full image' /></a> |
| The event list exported to a text file                       | <a href='http://wiki.pynetstation.googlecode.com/hg/img/event_list_exported_003.png'><img src='http://wiki.pynetstation.googlecode.com/hg/img/t_event_list_exported_003.png' alt='link to the image' title='click to see the full image' /></a> |


  * An important hint : **"Opt-click" on any "unexpanded" event marker entries in the event list to get them all unwrapped -- otherwise the field values won't be exported to the text file .** In other words, _only "unwrapped"_ (as on the screenshot) fields get exported to the text file.
  * Another hint is **not** to use the exporting utility written by EGI -- as it seems to **not** export the marker fields data .


Next: [Reference](Reference.md)
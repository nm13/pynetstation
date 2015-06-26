I have no intention to preserve any bugs in my code, so if you find one -- please [report the problem](http://code.google.com/p/pynetstation/issues/list), or [send a patch](http://code.google.com/p/pynetstation/source/checkout) (not sure if anonymous users can upload code, though), or [contact me directly](Contact.md) (**please use 'pynetstation' keyword in the subject** -- e.g. paste a link to the project page, [to the file of interest](http://code.google.com/p/pynetstation/source/browse/), or so on) .

But with Netstation situation is a bit different, so I list here all known "features" ( that may or may not be existing in your case ) along with the suggested workarounds, if they are available.



<a href='Hidden comment: 
...
'></a>

# 30000 events #

Apparently, in our version of the code there is a two-byte counter to store the event markers, what poses an obvious limitation on the maximum amount of the events one can have in a recording. ( It is 2<sup>15 or 2</sup>16 depending on whether that internal counter is a signed or an unsigned value. )

This limitation was confirmed via communication with EGI ( though I am not sure about the status of the statement ).

Practically it means that it might be impossible to open the recording with Netstation if the number of the events exceeds some internal limit (it is possible to _make_ such a recording, though, so I do not know if the internal counter goes to a negative value due to an overflow, or Netstation code just simply refuses to open e recording with maximum amount of events).

<i> The moral here is that the number of events we can record is limited, and it is better to keep it as small as possible ( if it is necessary to send a big list of timestamps during the recording session, consider sending <i>one</i> event that has a 'table' argument with many different named timestamps attached ) . </i>


# Buffer underflow problem #

While there is nothing special about the code and one may want by some reason to reimplement it from "scratch", be warned that it seems that at least in both our and [libnetstation](http://code.google.com/p/libnetstation/)'s author installations of Netstation the internal buffer that stores the received event is not cleared, so if one sends a "small" event after a "big" one simply following the described communication protocol, then, depending on the particular case, either part of the old information -- or some garbage -- would be recorded with the second "small" event as well.

To bypass that, we send some explicit "empty" information in the case if it is not provided ("empty" description string, etc).

<i> The moral here that you probably have nothing to worry about unless you want to re-implement the same code yourself ) </i>


# 32-bit timestamp limitation #

To the best of our understanding of the clock synchronization process, Netstation records down the 'remote' time along with the local time of the moment when it receives the synchronization message; later it simply adds the ('local' - 'remote') difference from any 'remote' timestamp value received with the event marker.

One of the small subtle problems here is that as Netstation stores the timestamps as 32-bit values, equal to amount of milliseconds since some "zero moment" (for Netstation this is the beginning of the session), we can't simply use ` int( time.time() * 1000 ) ` for the timestamp. Currently we use last billion of milliseconds from time.time() -- and check for overflow, that could happen _once_ in approx. every 10 days ; but may be we should use some internal timer and reset it on creation of the Netstation object.

<i> The moral of the story is that there is a small chance that once in 10 days there will be a ( correctly reported ) problem with the internal counter ; there is a list of possibilities to bypass this problem if it will really appear to be important (say, if one has to make a unique recording in conditions that one wouldn't be able to reproduce later); in that case, please look at the 'ms_localtime()' function code -- or contact me, the author . </i>


# Small bugs or corner cases #

There are some other small things one should know about the EGI hardware communication protocol if one wants to re-implement it :

  * the 'reversed' byte order for the case of the Intel architecture ( 'NTEL' byte order in the EGI terms ) applies only for integers, not for floating-point values ;
  * in the case of an error, the returned code is **not** 'Fss' as is stated in the documentation, but actually ( for protocol v.1 ) consists of **four** characters after 'F' ( of the form '+000', or '+001', etc )

<i>This information is useful only for module code support in the unlikely case of development of the next versions of the communication protocol and can be also safely ignored by the user . </i>
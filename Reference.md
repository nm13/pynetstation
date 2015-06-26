

As the reference is extracted from the Python code, I suggest to simply use IPython and follow the usual convention to ignore everything that starts with an underscore `_` -- i.e. treat it as "internal module variables or methods" .

Everything else generally should have associated help )

# class Netstation #
> """ Provides Python interface for a connection with the Netstation via a TCP/IP socket. """

## method _connect()_ (or _initialize()_) ##

Connect to the Netstaton machine. The arguments: the ip address of the Netstation computer, the NetStation app port number.

## method _disconnect()_ (or _finalize()_) ##

Close the connection.


## method _BeginSession()_ ##

Say 'hi!' to the server )

## method _EndSession()_ ##

Say 'bye' to the server.

## method _StartRecording()_ ##

Start recording )
Note that the possibility to set the record file size limit or timeout programmatically does not exist .

## method _StopRecording()_ ##


Stop recording. ( Another recording within the same session can be started with the BeginRecording() command if the session is not closed yet. )

( This possibility was not tested. )

## method _sync()_ ##

Communicate with NetStation in attempt to synchronize the clock

## method _send\_event()_ ##

Send an event ; note that before sending any events a sync() _must_ be called at least once .

Arguments:
  * 'id' -- a four-character identifier of the event ;
  * 'timestamp' -- the local time when event has happened, in milliseconds ; note that the "clock" used to produce the timestamp should be the same as for the sync() method, and, ideally, should be obtained via a call to the same function .
  * 'label' -- a string with any additional information, up to 256 characters .
  * 'description' -- more additional information can go here ( same limit applies ) .
  * 'table' -- a standard Python dictionary, where keys are 4-byte identifiers, not more than 256 in total ; there are no special limitations on the values, but the size of every value entry in bytes should not exceed 2 ^ 16 .



  * Note: due to peculiarity of the implementation, our particular version of NetStation was not able to record more than 2^15 events per session .

Next: [technical details](TechnicalDetails.md)
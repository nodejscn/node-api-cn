
Whenever an HTTP/2 `SETTINGS` frame is sent to a connected peer, the peer is
required to send an acknowledgement that it has received and applied the new
SETTINGS. By default, a maximum number of un-acknowledged `SETTINGS` frame may
be sent at any given time. This error code is used when that limit has been
reached.

<a id="ERR_HTTP2_OUT_OF_STREAMS"></a>

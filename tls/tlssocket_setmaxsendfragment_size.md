<!-- YAML
added: v0.11.11
-->

* `size` {number} The maximum TLS fragment size. The maximum value is `16384`.
  **Default:** `16384`.
* Returns: {boolean}

The `tlsSocket.setMaxSendFragment()` method sets the maximum TLS fragment size.
Returns `true` if setting the limit succeeded; `false` otherwise.

Smaller fragment sizes decrease the buffering latency on the client: larger
fragments are buffered by the TLS layer until the entire fragment is received
and its integrity is verified; large fragments can span multiple roundtrips
and their processing can be delayed due to packet loss or reordering. However,
smaller fragments add extra TLS framing bytes and CPU overhead, which may
decrease overall server throughput.


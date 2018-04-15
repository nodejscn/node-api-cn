<!-- YAML
added: v8.4.0
-->
Provides miscellaneous information about the current state of the
`Http2Stream`.

* Value: {Object}
  * `localWindowSize` {number} The number of bytes the connected peer may send
    for this `Http2Stream` without receiving a `WINDOW_UPDATE`.
  * `state` {number} A flag indicating the low-level current state of the
    `Http2Stream` as determined by nghttp2.
  * `localClose` {number} `true` if this `Http2Stream` has been closed locally.
  * `remoteClose` {number} `true` if this `Http2Stream` has been closed
    remotely.
  * `sumDependencyWeight` {number} The sum weight of all `Http2Stream`
    instances that depend on this `Http2Stream` as specified using
    `PRIORITY` frames.
  * `weight` {number} The priority weight of this `Http2Stream`.

A current state of this `Http2Stream`.


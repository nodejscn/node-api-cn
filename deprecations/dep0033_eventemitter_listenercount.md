<!-- YAML
changes:
  - version:
    - v6.12.0
    - v4.8.6
    pr-url: https://github.com/nodejs/node/pull/10116
    description: A deprecation code has been assigned.
  - version: v3.2.0
    pr-url: https://github.com/nodejs/node/pull/2349
    description: Documentation-only deprecation.
-->

Type: Documentation-only

The [`EventEmitter.listenerCount(emitter, eventName)`][] API is
deprecated. Please use [`emitter.listenerCount(eventName)`][] instead.


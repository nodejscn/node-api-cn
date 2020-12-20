<!-- YAML
added: v10.5.0
changes:
  - version:
    - v14.7.0
    pr-url: https://github.com/nodejs/node/pull/34057
    description: This class now inherits from `EventTarget` rather than
                 from `EventEmitter`.
-->

* 继承自: {EventEmitter}

Instances of the `worker.MessagePort` class represent one end of an
asynchronous, two-way communications channel. It can be used to transfer
structured data, memory regions and other `MessagePort`s between different
[`Worker`][]s.

With the exception of `MessagePort`s being [`EventEmitter`][]s rather
than [`EventTarget`][]s, this implementation matches [browser `MessagePort`][]s.


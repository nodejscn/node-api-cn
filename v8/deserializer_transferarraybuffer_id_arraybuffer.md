
* `id` {integer} A 32-bit unsigned integer.
* `arrayBuffer` {ArrayBuffer|SharedArrayBuffer} An `ArrayBuffer` instance.

Marks an `ArrayBuffer` as having its contents transferred out of band.
Pass the corresponding `ArrayBuffer` in the serializing context to
[`serializer.transferArrayBuffer()`][] (or return the `id` from
[`serializer._getSharedArrayBufferId()`][] in the case of `SharedArrayBuffer`s).


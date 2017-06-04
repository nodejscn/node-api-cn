
* `id` {integer} A 32-bit unsigned integer.
* `arrayBuffer` {ArrayBuffer} An `ArrayBuffer` instance.

Marks an `ArrayBuffer` as havings its contents transferred out of band.
Pass the corresponding `ArrayBuffer` in the deserializing context to
[`deserializer.transferArrayBuffer()`][].


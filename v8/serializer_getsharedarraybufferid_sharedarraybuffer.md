
* `sharedArrayBuffer` {SharedArrayBuffer}

This method is called when the serializer is going to serialize a
`SharedArrayBuffer` object. It must return an unsigned 32-bit integer ID for
the object, using the same ID if this `SharedArrayBuffer` has already been
serialized. When deserializing, this ID will be passed to
[`deserializer.transferArrayBuffer()`][].

If the object cannot be serialized, an exception should be thrown.

This method is not present on the `Serializer` class itself but can be provided
by subclasses.


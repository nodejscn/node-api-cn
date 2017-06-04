
* Returns: {Buffer}

Read raw bytes from the deserializer’s internal buffer. The `length` parameter
must correspond to the length of the buffer that was passed to
[`serializer.writeRawBytes()`][].
For use inside of a custom [`deserializer._readHostObject()`][].


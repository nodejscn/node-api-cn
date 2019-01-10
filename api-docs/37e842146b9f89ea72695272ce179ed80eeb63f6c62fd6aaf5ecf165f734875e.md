
* `sharedArrayBuffer` {SharedArrayBuffer}

当序列化机制将要序列化一个`ShareArrayBuffer`对象时会调用此方法。它必须为这对象返回一个32位无符号整型的ID，但若这个对象已被序列化过，则返回上一次序列化时所分配的ID。这个ID会在对象被反序列化时传入[`deserializer.transferArrayBuffer()`][]中。

如果对象不能被序列化，则抛出异常。

`Serializer`类本身不包含此方法，但可以在其子类中设置它。

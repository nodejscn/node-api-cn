
This method is called to read some kind of host object, i.e. an object that is
created by native C++ bindings. If it is not possible to deserialize the data,
a suitable exception should be thrown.

This method is not present on the `Deserializer` class itself but can be
provided by subclasses.


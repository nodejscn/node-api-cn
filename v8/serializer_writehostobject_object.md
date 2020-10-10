
* `object` {Object}

This method is called to write some kind of host object, i.e. an object created
by native C++ bindings. If it is not possible to serialize `object`, a suitable
exception should be thrown.

This method is not present on the `Serializer` class itself but can be provided
by subclasses.


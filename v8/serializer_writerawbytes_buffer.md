
* `buffer` {Buffer|Uint8Array}

将原始字节写入序列化机制的内部缓冲区中。反序列化机制会有对应的方法来获得缓冲区的长度。 
此方法用于一个自定义的[`serializer._writeHostObject()`][]中。

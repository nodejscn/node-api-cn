
`stream.Readable` 类扩展并实现了[Readable][]。 

用户实现的自定义可读流 *必须* 调用`new stream.Readable([options])`
构造函数并且实现`readable._read()`方法。


<!-- YAML
added: v0.1.92
-->

* 继承自: {stream.Writable}

`Verify` 类是一个实用工具，用于验证签名。
它可以通过以下两种方式之一使用：

- 作为可写的[流][stream]，其中使用写入的数据来验证提供的签名。
- 使用 [`verify.update()`] 和 [`verify.verify()`] 方法来验证签名。

[`crypto.createVerify()`] 方法用于创建 `Verify` 实例。
不能使用 `new` 关键字直接地创建 `Verify` 对象。

有关示例，请参见 [`Sign`]。


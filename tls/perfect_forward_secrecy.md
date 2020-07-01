
<!-- type=misc -->

术语“[前向保密][Forward Secrecy]”或“完全前向保密”是一种密钥协商（或称做密钥交换）方法。
通过这种方法,客户端与服务端在当前会话中，协商一个临时生成的密钥进行对称加密的密钥交换。
这意味着即使服务器端私钥发生泄漏，窃密者与攻击者也无法解密通信内容，除非他们能得到当前会话的临时密钥。

TLS/SSL 握手时，使用完全前向即每次会话都会随机生成一个临时密钥对用于对称加密密钥协商(区别于每次会话都是用相同的密钥)。
实现这个技术的密钥交换算法称为“ephemeral”。

当前最常用的两种实现完全前向保密的算法（注意算法结尾的"E"）：

* [DHE] - 使用临时密钥的 Diffie Hellman 密钥交换算法。
* [ECDHE] - 使用临时密钥的椭圆曲线 Diffie Hellman 密钥交换算法。

使用临时密钥会带来性能损失，因为密钥生成的过程十分消耗 CPU 计算性能。

如需使用完全前向加密，例如使用 `tls` 模块的 `DHE` 算法，使用之前需要生成一个 Diffie-Hellman 参数并将其用 `dhparam` 声明在 [`tls.createSecureContext()`][] 中。
如下例子展示了如何使用 OpenSSL 命令生成参数：

```bash
openssl dhparam -outform PEM -out dhparam.pem 2048
```
如需使用 `ECDHE` 算法，则不需要生成 Diffie-Hellman 参数，因为可以使用默认的 ECDHE 曲线。
在创建 TLS Server 时，可使用 `ecdhCurve` 属性声明服务器支持的曲线名词，详请参见 [`tls.createServer()`]。

完全前向保密在 TLSv1.2 之前是可选的，但它不是 TLSv1.3 的可选项，因为所有 TLSv1.3 密码套件都使用 ECDHE。


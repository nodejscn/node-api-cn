
<!-- type=misc -->

术语“前向保密”或“[完全前向保密]”是一种密钥协商（或称做密钥交换）方法.
通过这种方法,客户端与服务端在当前会话中,协商一个临时生成的密钥进行对称加密的密钥交换.
这意味着即使服务器端私钥发生泄漏,窃密者与攻击者也无法解密通信内容,除非他们能得到当前会话的临时密钥.

TLS/SSL 握手时,使用完全前向即每次会话都会随机生成一个临时密钥对用于对称加密密钥协商(区别于每次会话都是用相同的密钥).
实现这个技术的密钥交换算法都带有一个E,即ephemeral.

当前最常用的两种实现完全前向保密的算法(注意算法结尾的"E"):

* [DHE] - 使用临时密钥的Diffie Hellman密钥交换算法.
* [ECDHE] - 使用临时密钥的椭圆曲线Diffie Hellman密钥交换算法.

使用临时密钥会带来性能损失,因为密钥生成的过程十分消耗CPU计算性能.

如需使用完全前向加密,例如使用`tls`模块的`DHE`算法,使用之前需要生成一个Diffie-Hellman
参数并将其用`dhparam`声明在[`tls.createSecureContext()`][]中.如下例子展示了如何使用
OpenSSL命令生成参数:

```sh
openssl dhparam -outform PEM -out dhparam.pem 2048
```
如需使用`ECDHE`算法,则不需要生成Diffie-Hellman,因为可以使用默认的ECDHE曲线.
在创建TLS Server时,可使用`ecdhCurve`属性声明服务器支持的曲线名词.详请参考[`tls.createServer()`].

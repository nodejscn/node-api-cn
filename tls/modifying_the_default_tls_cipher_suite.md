
Node.js 构造时包含了默认的 TLS 开启和关闭的加密组件。
目前默认的加密组件是：

```txt
ECDHE-RSA-AES128-GCM-SHA256:
ECDHE-ECDSA-AES128-GCM-SHA256:
ECDHE-RSA-AES256-GCM-SHA384:
ECDHE-ECDSA-AES256-GCM-SHA384:
DHE-RSA-AES128-GCM-SHA256:
ECDHE-RSA-AES128-SHA256:
DHE-RSA-AES128-SHA256:
ECDHE-RSA-AES256-SHA384:
DHE-RSA-AES256-SHA384:
ECDHE-RSA-AES256-SHA256:
DHE-RSA-AES256-SHA256:
HIGH:
!aNULL:
!eNULL:
!EXPORT:
!DES:
!RC4:
!MD5:
!PSK:
!SRP:
!CAMELLIA
```
默认加密组件可以使用 `--tls-cipher-list` 命令进行替换。
比如，生成 `ECDHE-RSA-AES128-GCM-SHA256:!RC4` 的 TLS 加密组件：

```sh
node --tls-cipher-list="ECDHE-RSA-AES128-GCM-SHA256:!RC4"
```

默认的加密组件也可以通过客户端或者服务器的 [`tls.createSecureContext()`] 方法的 `ciphers` 选项来进行替换，[`tls.createServer()`] 方法和 [`tls.connect()`] 方法也可以使用 `ciphers` 选项进行设置，当然也可以在创建一个 [`tls.TLSSocket`] 时设置。

查询 [OpenSSL 加密列表格式文档][OpenSSL cipher list format documentation]获取格式的具体细节。

Node.js 包含的默认的加密组件是经过精心挑选，能体现目前最好的安全实践和最低风险。
改变默认的加密组件可以对应用的安全性有重大的影响。
`--tls-cipher-list` 开关和 `ciphers` 选项应该只在必要的时候使用。

默认加密组件倾向使用 GCM 加密作为 [Chrome 现代加密设置][Chrome's 'modern cryptography' setting]的选项，也倾向使用 ECDHE 和 DHE 加密算法实现完美的前向安全，同时向后兼容。

依据[特殊攻击影响更大位数的 AES 密钥][specific attacks affecting larger AES key sizes]，128 位的 AES 密钥优先于 192 位和 256 位的 AES 密钥。

老的客户端依赖不安全的 RC4 或者基于 DES 的加密（比如 IE6）不能用默认配置完成握手的过程。
如果必须支持这些客户端，[TLS 推荐规范][TLS recommendations]也许可以提供兼容的加密组件。
欲知更多的格式的细节请参阅 [OpenSSL 加密列表格式文档][OpenSSL cipher list format documentation]。


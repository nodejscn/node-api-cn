
Node.js 构造时包含了默认的 TLS 开启和关闭的加密套件。在构建自己的Node.js分发版本时，
可以配置默认支持的加密套件列表。
下表中的命令可以查看默认的加密套件：
```console
node -p crypto.constants.defaultCoreCipherList | tr ':' '\n'
TLS_AES_256_GCM_SHA384
TLS_CHACHA20_POLY1305_SHA256
TLS_AES_128_GCM_SHA256
ECDHE-RSA-AES128-GCM-SHA256
ECDHE-ECDSA-AES128-GCM-SHA256
ECDHE-RSA-AES256-GCM-SHA384
ECDHE-ECDSA-AES256-GCM-SHA384
DHE-RSA-AES128-GCM-SHA256
ECDHE-RSA-AES128-SHA256
DHE-RSA-AES128-SHA256
ECDHE-RSA-AES256-SHA384
DHE-RSA-AES256-SHA384
ECDHE-RSA-AES256-SHA256
DHE-RSA-AES256-SHA256
HIGH
!aNULL
!eNULL
!EXPORT
!DES
!RC4
!MD5
!PSK
!SRP
!CAMELLIA
```

默认加密组件可以使用 [`--tls-cipher-list`] 命令进行替换（直接或通过 [`NODE_OPTIONS`] 环境变量）。
比如，生成 `ECDHE-RSA-AES128-GCM-SHA256:!RC4` 的 TLS 加密组件：

```bash
node --tls-cipher-list='ECDHE-RSA-AES128-GCM-SHA256:!RC4' server.js

export NODE_OPTIONS=--tls-cipher-list='ECDHE-RSA-AES128-GCM-SHA256:!RC4'
node server.js
```

默认的加密组件也可以通过客户端或者服务器的 [`tls.createSecureContext()`] 方法的 `ciphers` 选项来进行替换，[`tls.createServer()`] 方法和 [`tls.connect()`] 方法也可以使用 `ciphers` 选项进行设置，当然也可以在创建一个 [`tls.TLSSocket`] 时设置。

密码列表可以包含 TLSv1.3 密码套件名称的混合，以 `'TLS_'` 开头的密码，以及 TLSv1.2 及以下密码套件的规范。 
TLSv1.2 密码支持传统规范格式，有关详细信息，请参见 OpenSSL [密码列表格式][cipher list format]文档，但这些规范不适用于 TLSv1.3 密码。 
只能通过在密码列表中包含其全名来启用 TLSv1.3 套件。 
例如，它们不能通过使用传统的 TLSv1.2 `'EECDH'`或 `'!EECDH'` 规范来启用或禁用。

尽管 TLSv1.3 和 TLSv1.2 密码套件的相对顺序，TLSv1.3 协议明显比 TLSv1.2 更安全，并且如果握手表明它受支持，并且如果有任何 TLSv1.3 密码套件已启用，将始终选择 TLSv1.2 以上。

Node.js 包含的默认的加密组件是经过精心挑选，能体现目前最好的安全实践和最低风险。
改变默认的加密组件可以对应用的安全性有重大的影响。
`--tls-cipher-list` 开关和 `ciphers` 选项应该只在必要的时候使用。

默认加密组件倾向使用 GCM 加密作为 [Chrome 现代加密设置][Chrome's 'modern cryptography' setting]的选项，也倾向使用 ECDHE 和 DHE 加密算法实现完美的前向安全，同时向后兼容。

依据[特殊攻击影响更大位数的 AES 密钥][specific attacks affecting larger AES key sizes]，128 位的 AES 密钥优先于 192 位和 256 位的 AES 密钥。

老的客户端依赖不安全的 RC4 或者基于 DES 的加密（比如 IE6）不能用默认配置完成握手的过程。
如果必须支持这些客户端，[TLS 推荐规范][TLS recommendations]也许可以提供兼容的加密组件。
欲知更多的格式的细节请参见 OpenSSL [加密列表格式][cipher list format]文档。

只有 5 种 TLSv1.3 密码套件：
- `'TLS_AES_256_GCM_SHA384'`
- `'TLS_CHACHA20_POLY1305_SHA256'`
- `'TLS_AES_128_GCM_SHA256'`
- `'TLS_AES_128_CCM_SHA256'`
- `'TLS_AES_128_CCM_8_SHA256'`

默认情况下启用前 3 个。 
TLSv1.3 支持最后 2 个基于 `CCM` 的套件，因为它们在受约束的系统上可能有更好的性能，但默认情况下它们不会启用，因为它们提供的安全性较低。


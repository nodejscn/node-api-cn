<!-- YAML
added: v0.1.94
changes:
  - version: v11.6.0
    pr-url: https://github.com/nodejs/node/pull/24234
    description: The `key` argument can now be a `KeyObject`.
  - version: v11.2.0
    pr-url: https://github.com/nodejs/node/pull/24081
    description: The cipher `chacha20-poly1305` is now supported.
  - version: v10.10.0
    pr-url: https://github.com/nodejs/node/pull/21447
    description: Ciphers in OCB mode are now supported.
  - version: v10.2.0
    pr-url: https://github.com/nodejs/node/pull/20235
    description: The `authTagLength` option can now be used to produce shorter
                 authentication tags in GCM mode and defaults to 16 bytes.
  - version: v9.9.0
    pr-url: https://github.com/nodejs/node/pull/18644
    description: The `iv` parameter may now be `null` for ciphers which do not
                 need an initialization vector.
-->

* `algorithm` {string}
* `key` {string | Buffer | TypedArray | DataView | KeyObject}
* `iv` {string | Buffer | TypedArray | DataView | null}
* `options` {Object} [`stream.transform` 的选项][`stream.transform` options]。
* 返回: {Cipher}

使用给定的 `algorithm`、`key` 和初始化向量（`iv`）创建并返回一个 `Cipher` 对象。

`options` 参数控制流的行为，它是可选的，除非使用 CCM 或 OCB 模式的密码（例如 `'aes-128-ccm'`）。
在这种情况下，必须使用 `authTagLength` 选项，并以字节为单位指定身份验证标签的长度，参阅 [CCM 模式][CCM mode]。
在 GCM 模式中，不需要 `authTagLength` 选项，但可以使用它来设置将会由 `getAuthTag()` 返回的身份验证标签的长度，默认为 16 个字节。

`algorithm` 取决于 OpenSSL，例如 `'aes192'` 等。
在 OpenSSL 的最新版本中，`openssl list -cipher-algorithms`（在较旧版本的 OpenSSL 中是 `openssl list-cipher-algorithms`）将会显示可用的密码算法。

`key` 是 `algorithm` 使用的原始密钥，`iv` 是[初始化向量][initialization vector]。
两个参数都必须是 `'utf8'` 编码的字符串、[Buffer][`Buffer`]、`TypedArray` 或 `DataView`。
`key` 可以是 `secret` 类型的 [`KeyObject`]。
如果密码不需要初始化向量，则 `iv` 可以为 `null`。

初始化向量应该是不可预测的且唯一的，理想情况下，它们在密码上是随机的。
它们不必是私密的：IV 通常只是添加到未加密的密文消息中。
它们必须是不可预测的且唯一的，但不一定是私密的，这听起来似乎是矛盾的。
记住，攻击者必须无法提前预测给定的 IV 将会是什么。


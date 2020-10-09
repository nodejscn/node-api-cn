
<!-- type=misc -->

TLS-PSK(Pre-Shared-Key:预共享密钥)是一种身份认证方式，有别于普通的基于证书认证的身份认证，
TLS握手中，PSK使用预共享密钥来代替证书认证，提供多样化的认证手段。TLS-PSK和PKI（公钥基础设施）
不是互斥的，客户端和服务器端在密钥套件的协商过程中，可以共用两种或者使用其中一种方式来完成协商。

仅当通信双方有安全的密钥共享信道时，才考虑使用TLS-PSK来进行身份认证。基于这个原因，PSK
不会替换PKI在TLS中的重要用途。近年来，在OpenSSL的实现中发现了许多TLS-PSK的安全缺陷，因为
它仅仅在少数的应用中使用，所以，在使用PSK密钥套件前，请充分考虑替代方案。在[RFC 4086][https://tools.ietf.org/html/rfc4086]
中讨论了生成PSK过程中，充分无序的密钥是非常重要的，从固定密码和低无序性源中获取预共享密钥
是不安全的。

默认情况下，PSK相关的密钥套件是被禁用的，如果需要使用基于TLS-PSK密钥套件，需要使用`ciphers`参数显式声明。
使用`openssl ciphers -v 'PSK'`可以查询到所有可用的基于PSK密钥套件。所有TLS 1.3协议支持的密钥套件均是
合法的PSK密钥套件，但当前仅支持SHA256摘要算法的套件，可以通过`openssl ciphers -v -s -tls1_3 -psk`
查询符合要求的密钥套件。

根据[RFC 4279][https://tools.ietf.org/html/rfc4279]，PSK标识符最大长度应大于128bytes，PSK密钥最大长度应大于64bytes。
在OpenSSL 1.1.0版本中，最大PSK标识符长度为128byte，最大PSK密钥长度为256btyes。

因为底层OpenSSL API的限制，当前的实现不支持异步PSK回调。

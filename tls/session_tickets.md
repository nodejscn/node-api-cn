
服务器加密整个会话状态，并将其发送给客户端，被称为“票据（ticket）”。当需要复用会话时，客户端
在握手阶段将ticket发送给服务器。这种机制的优点是服务器端不需要缓存会话状态。如果基于任何
原因（包括解密ticket内容失败，ticket信息超时等情况），服务器不使用ticket，则会新建一个会话，并
发送新的ticket给客户端，详见[RFC 5077][]。

基于tickets的会话复用方式正在被越来越多的主流浏览器支持。

在Node.js中，客户端的两种会话复用使用相同的API。在调试时，如果[`tls.TLSSocket.getTLSTicket()`][]
返回了会话信息，并且会话信息中包含ticket，则使用了Session Ticket会话复用，
否则使用了Session ID会话复用。

在TLS1.3中，需要注意服务器可能会发送多个ticket，这会触发多个`'session'`事件，详见[`'session'`][]
事件中的介绍。

单个服务器使用session ticket会话复用不需要特别的实现，但如果需要在服务器重启后或者在使用
负载均衡的情况下，任然能够复用成功，则所有服务器必须要使用相同的密钥来生成ticket。这个密钥
由三个16字节的密钥组成，但在API实现中，为了方便使用了一个48字节的缓存保存。

服务器实例使用[`server.getTicketKeys()`][]可以获取ticket密钥，并将其分发给其他服务器。
但出于安全考虑，最好是生成48字节随机的数据并通过 `tls.createServer()`][]的`ticketKeys`
参数来设置。密钥最好定时重新生成并通过[`server.setTicketKeys()`][]在服务器中更新。

Session ticket是TLS协商过程的加密密钥之一，因此ticket***必须安全的存储***。在TLS1.2及TLS1.2以下版本，
如果为了妥协而使用相同的ticket加密所有会话，则最好不要将ticket存储在磁盘上，并且应该定期更新ticket的生成密钥。

如果客户端支持ticket，则服务器会在TLS协商过程中发送。如果服务器端需要禁用ticket，需要在
`secureOptions`提供`require('constants').SSL_OP_NO_TICKET`来禁用。

Session ID和session ticket会话复用都有超时，超时后服务器将创建新的会话。可以通过[`tls.createServer()`][]
的`sessionTimeout`来设置超时时间。

对上述所有机制，当会话复用失败时，服务器会创建一个新的会话，这不会导致TLS/HTTPS连接失败，因为TLS性能的影响，这显然不需要通知到TLS/HTTPS连接层面。
在Openssl命令行中，可以通过如下方式验证服务器是否支持会话复用。可以使用`openssl s_client`的`-reconnect`参数, 例如：

```console
$ openssl s_client -connect localhost:443 -reconnect
```

查看调试输出，第一条连接应该包括一个"New"字段，例如：

```text
New, TLSv1.2, Cipher is ECDHE-RSA-AES128-GCM-SHA256
```

接下来的连接应该包括"Reused"字段，例如：

```text
Reused, TLSv1.2, Cipher is ECDHE-RSA-AES128-GCM-SHA256
```


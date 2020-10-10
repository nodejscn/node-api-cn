
<!-- type=misc -->
ALPN (Application-Layer Protocol Negotiation Extension,应用层协议协商),
NPN (Next Protocol Negotiation,下一代协议协商) , 
SNI (Server Name Indication,服务器名称指示)是三个TLS拓展:

* ALPN/NPN - 允许一个TLS服务器使用多个版本的HTTP协议 (HTTP, SPDY, HTTP/2).
* SNI - 允许一个TLS服务器支持多个主机名以及证书.

*注意*: 应优先使用ALPN而非NPN,因为NPN拓展从未正式定义或记录,一般不建议使用.

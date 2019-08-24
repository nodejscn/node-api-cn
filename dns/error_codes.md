
每次 DNS 查询可能返回以下错误码之一:

-  `dns.NODATA`: DNS 服务器返回没有数据。
-  `dns.FORMERR`: DNS 服务器查询格式错误。
-  `dns.SERVFAIL`: DNS 服务器返回常规失败。
-  `dns.NOTFOUND`: 域名未找到。
-  `dns.NOIMP`: DNS 服务器未实行请求的操作。
-  `dns.REFUSED`: DNS 服务器拒绝查询。
-  `dns.BADQUERY`:  格式错误的 DNS 查询。
-  `dns.BADNAME`: 格式错误的主机名。
-  `dns.BADFAMILY`: 不提供的地址族。
-  `dns.BADRESP`: 格式错误的 DNS 回复。
-  `dns.CONNREFUSED`: 无法连接 DNS 服务器。
-  `dns.TIMEOUT`: 连接 DNS 服务器超时。
-  `dns.EOF`: 文件结束。
-  `dns.FILE`: 读取文件错误。
-  `dns.NOMEM`: 内存溢出。
-  `dns.DESTRUCTION`: 通道正被销毁。
-  `dns.BADSTR`: 格式错误的字符串。
-  `dns.BADFLAGS`: 指定的标记非法。
-  `dns.NONAME`: 给定的主机名不是数字。
-  `dns.BADHINTS`: 指定提示标志非法。
-  `dns.NOTINITIALIZED`: 未执行 c-ares 库初始化。
-  `dns.LOADIPHLPAPI`: 加载 `iphlpapi.dll` 错误。
-  `dns.ADDRGETNETWORKPARAMS`: 找不到 `GetNetworkParams` 函数。
-  `dns.CANCELLED`: DNS 查询取消。


# Type Client

客户端是HTTP客户端。它的初始值（DefaultClient）是使用DefaultTransport的可用客户端。

客户端的传输通常具有内部状态（缓存的TCP连接），因此应重新使用客户端，而不是根据需要创建客户端。客户端可以安全地被多个goroutine并发使用。

客户端比RoundTripper（例如Transport）更高级别，并且还处理HTTP详细信息，例如cookie和重定向。



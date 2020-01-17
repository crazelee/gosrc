# Type Server

## 结构体

```
type Server struct {
	Addr    string  // 监听地址
	Handler Handler // 路由
	TLSConfig *tls.Config  // https 配置
	ReadTimeout time.Duration   // 读取请求最大时长
	ReadHeaderTimeout time.Duration   // 读取header超时设置
	WriteTimeout time.Duration     // 写入超时设置
	IdleTimeout time.Duration  // 链接空闲时长
	MaxHeaderBytes int    // header 头最大长度
	//HTTP2.0协商
	TLSNextProto map[string]func(*Server, *tls.Conn, Handler)
	// 链接状态回调，根据状态改变执行对应的回调函数
	ConnState func(net.Conn, ConnState)
	// 自定义错误日志
	ErrorLog *log.Logger
	// 一个请求进来指定的基本context
	BaseContext func(net.Listener) context.Context
	// 给新的请求提供的一个可修改context的方法
	ConnContext func(ctx context.Context, c net.Conn) context.Context

	disableKeepAlives int32     // accessed atomically.
	inShutdown        int32     // accessed atomically (non-zero means we're in Shutdown)
	nextProtoOnce     sync.Once // guards setupHTTP2_* init
	nextProtoErr      error     // result of http2.ConfigureServer if used

	mu         sync.Mutex
	listeners  map[*net.Listener]struct{}  // 监听器，路由
	activeConn map[*conn]struct{}
	doneChan   chan struct{}
	onShutdown []func()
}
```

## func Close()
关闭服务

## func (srv *Server) ListenAndServe() error
监听并开启http服务

1、开启监听
2、调用server


## func (srv *Server) ListenAndServeTLS(certFile, keyFile string) error
开启HTTPS服务

## func (srv *Server) RegisterOnShutdown(f func())
平滑关闭，在关闭服务之前回调指定方法

## func (srv *Server) Serve(l net.Listener) error
接受http listener，开启listener服务                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            listener，开启listener服务

监听链接，每条请求都会新生成一个goroutine去处理请求

## func (srv *Server) ServeTLS(l net.Listener, certFile, keyFile string) error
接受https listener，开启listener服务

解析证书路径，秘钥路径，new TLS listener 去调用Server

## func (srv *Server) Shutdown(ctx context.Context) error
平滑关闭


## (srv *Server) Serve(l net.Listener) error
接收在监听器listener的请求，为每一个请求创建一个新的goroutine。
goroutine读取请求并且调用server.Handler进行回复。

服务总是返回非零错误并关闭listener。

#### 流程：
1、解析请求地址
2、


可参考
https://learnku.com/docs/build-web-application-with-golang/how-033-go-makes-web-work/3170


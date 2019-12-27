# net http

# 常量

路径: method.go

- HTTP请求方法

代码实例：

    const (
        MethodGet     = "GET"
	    MethodHead    = "HEAD"
	    MethodPost    = "POST"
	    MethodPut     = "PUT"
	    MethodPatch   = "PATCH" // RFC 5789
	    MethodDelete  = "DELETE"
	    MethodConnect = "CONNECT"
	    MethodOptions = "OPTIONS"
	    MethodTrace   = "TRACE"
    )

路径: status.go

- HTTP请求状态码

代码实例：

    const (
        StatusContinue           = 100 // RFC 7231, 6.2.1
        StatusSwitchingProtocols = 101 // RFC 7231, 6.2.2
        StatusProcessing         = 102 // RFC 2518, 10.1
        StatusEarlyHints         = 103 // RFC 8297
    
        StatusOK                   = 200 // RFC 7231, 6.3.1
        StatusCreated              = 201 // RFC 7231, 6.3.2
        StatusAccepted             = 202 // RFC 7231, 6.3.3
        StatusNonAuthoritativeInfo = 203 // RFC 7231, 6.3.4
        StatusNoContent            = 204 // RFC 7231, 6.3.5
        StatusResetContent         = 205 // RFC 7231, 6.3.6
        StatusPartialContent       = 206 // RFC 7233, 4.1
        StatusMultiStatus          = 207 // RFC 4918, 11.1
        StatusAlreadyReported      = 208 // RFC 5842, 7.1
        StatusIMUsed               = 226 // RFC 3229, 10.4.1
    
        StatusMultipleChoices   = 300 // RFC 7231, 6.4.1
        StatusMovedPermanently  = 301 // RFC 7231, 6.4.2
        StatusFound             = 302 // RFC 7231, 6.4.3
        StatusSeeOther          = 303 // RFC 7231, 6.4.4
        StatusNotModified       = 304 // RFC 7232, 4.1
        StatusUseProxy          = 305 // RFC 7231, 6.4.5
        _                       = 306 // RFC 7231, 6.4.6 (Unused)
        StatusTemporaryRedirect = 307 // RFC 7231, 6.4.7
        StatusPermanentRedirect = 308 // RFC 7538, 3
    
        StatusBadRequest                   = 400 // RFC 7231, 6.5.1
        StatusUnauthorized                 = 401 // RFC 7235, 3.1
        StatusPaymentRequired              = 402 // RFC 7231, 6.5.2
        StatusForbidden                    = 403 // RFC 7231, 6.5.3
        StatusNotFound                     = 404 // RFC 7231, 6.5.4
        StatusMethodNotAllowed             = 405 // RFC 7231, 6.5.5
        StatusNotAcceptable                = 406 // RFC 7231, 6.5.6
        StatusProxyAuthRequired            = 407 // RFC 7235, 3.2
        StatusRequestTimeout               = 408 // RFC 7231, 6.5.7
        StatusConflict                     = 409 // RFC 7231, 6.5.8
        StatusGone                         = 410 // RFC 7231, 6.5.9
        StatusLengthRequired               = 411 // RFC 7231, 6.5.10
        StatusPreconditionFailed           = 412 // RFC 7232, 4.2
        StatusRequestEntityTooLarge        = 413 // RFC 7231, 6.5.11
        StatusRequestURITooLong            = 414 // RFC 7231, 6.5.12
        StatusUnsupportedMediaType         = 415 // RFC 7231, 6.5.13
        StatusRequestedRangeNotSatisfiable = 416 // RFC 7233, 4.4
        StatusExpectationFailed            = 417 // RFC 7231, 6.5.14
        StatusTeapot                       = 418 // RFC 7168, 2.3.3
        StatusMisdirectedRequest           = 421 // RFC 7540, 9.1.2
        StatusUnprocessableEntity          = 422 // RFC 4918, 11.2
        StatusLocked                       = 423 // RFC 4918, 11.3
        StatusFailedDependency             = 424 // RFC 4918, 11.4
        StatusTooEarly                     = 425 // RFC 8470, 5.2.
        StatusUpgradeRequired              = 426 // RFC 7231, 6.5.15
        StatusPreconditionRequired         = 428 // RFC 6585, 3
        StatusTooManyRequests              = 429 // RFC 6585, 4
        StatusRequestHeaderFieldsTooLarge  = 431 // RFC 6585, 5
        StatusUnavailableForLegalReasons   = 451 // RFC 7725, 3
    
        StatusInternalServerError           = 500 // RFC 7231, 6.6.1
        StatusNotImplemented                = 501 // RFC 7231, 6.6.2
        StatusBadGateway                    = 502 // RFC 7231, 6.6.3
        StatusServiceUnavailable            = 503 // RFC 7231, 6.6.4
        StatusGatewayTimeout                = 504 // RFC 7231, 6.6.5
        StatusHTTPVersionNotSupported       = 505 // RFC 7231, 6.6.6
        StatusVariantAlsoNegotiates         = 506 // RFC 2295, 8.1
        StatusInsufficientStorage           = 507 // RFC 4918, 11.5
        StatusLoopDetected                  = 508 // RFC 5842, 7.2
        StatusNotExtended                   = 510 // RFC 2774, 7
        StatusNetworkAuthenticationRequired = 511 // RFC 6585, 6
    )

路径: server.go

代码实例：

    // HTTP 最大请求头
    const DefaultMaxHeaderBytes = 1 << 20 // 1 MB （1048576）
    
    //MaxIdleConns限制最大keep-alive的连接数，超出的连接会被关闭掉。
    const DefaultMaxIdleConnsPerHost = 2
    
## func CanonicalHeaderKey(s string) string

路径：

- header.go

参数列表

- s 需要做标准化的http header字符串 

返回值：

- 返回按照http协议定义的标准化字符串

功能说明：
这个函数返回一个规范好的标准的http header字符串。
标准化的http header 字符串格式为：
第一个字母和跟着“-”字符后面的第一个字母大写，剩下的字符全部小写。
举个例子：
对于一个http头（header） "accept-encoding" 来说，
规范好的标准化格式就是
"Accept-Encoding"。

代码实例：

    package main

    import (
        "fmt"
	    "net/http"
    )

    func main() {
	    fmt.Println(http.CanonicalHeaderKey("accept-encoding"))
	    //Accept-Encoding
	    fmt.Println(http.CanonicalHeaderKey("accept-Language"))
	    //Accept-Language
    }

## func DetectContentType(data []byte) string

路径：

- sniff.go

参数列表

- data 需要检测类型的数据 

返回值：

- 返回检测好的MIME类型。如果不能检测到任何MIME类型，返回"application/octet-stream"。

功能说明：

该函数实现了一个算法，用来检测指定的数据是否符合http://mimesniff.spec.whatwg.org/所定义的MIME类型。
该函数最多需要数据的前512个字节。
该函数总是会返回一个有效的MIME类型。
如果它不能够识别数据，将会返回"application/octet-stream"。

代码实例

    package main
	    import (
		"fmt"
		"net/http"
	)

	func main() {
		var notingData []byte = []byte{0x01, 0x02}
		var gifData []byte = []byte{0x01, 0x02}				
		fmt.Println(http.DetectContentType(notingData))
		fmt.Println(http.DetectContentType(gifData))
	}

##func Error(w ResponseWriter, error string, code int) 

参数

- w 响应的写入器
- error 用户定义的错误信息
- code  用户定义的http代码

返回值

- 无

函数功能 

- 该函数通过一个ResponseWriter对象输出指定的错误信息和HTTP代码。

例子

    package main
	
	import (
		_ "io"
		"log"
		"net/http"
	)
	
	func HelloServer(w http.ResponseWriter, req *http.Request) {
		// 输出用户自定义错误
		http.Error(w, "this is a error", 404)
	}
	
	func main() {
		// 指定当用户访问 http://www.xxx.com:mmmm/hello 的时候(注意，请不要在hello后面加上/变成hello/)
		// 调用HelloServer这个函数来处理
		http.HandleFunc("/hello", HelloServer)
	
		// 如果顺利的话，你的浏览器会输出 this is a error，并且状态码为404
		err := http.ListenAndServe(":8888", nil)
		if err != nil {
			log.Fatal("ListenAndServe: ", err)
		}
	}

## func Handle(pattern string, handler Handler) 

参数

- pattern 需要匹配的pattern，比如/hello, /index.php , /index.aspx等等
- handler 实际响应该pattern的server

返回值

- 无

函数功能 

- 该函数在缺省的服务器路由（DefaultServeMux）中注册一个函数。当一个请求request进来的时候，缺省的服务器路由会依次根据ServeMux.m中的string（路由表达式）来一个一个匹配。文档（服务器路由）ServeMux解释了路由表达式是如何被匹配的。

例子

    package main
    
    import (
        "log"
        "net/http"
    )
    
    type HiServer struct {
    }
    
    func (server HiServer) ServeHTTP(w http.ResponseWriter, r *http.Request) {
        w.Write([]byte("say hi"))
    }
    
    type HelloServer struct {
    }
    
    func (server HelloServer) ServeHTTP(w http.ResponseWriter, r *http.Request) {
        w.Write([]byte("say hello"))
    }
    
    func main() {
        var hi HiServer
        http.Handle("/hi", hi)
    
        var hello HelloServer
        http.Handle("/hello", hello)
    
        log.Fatal(http.ListenAndServe("localhost:9000", nil))
    }

## HandleFunc(pattern string, handler func(ResponseWriter, *Request))

参数

- pattern 需要匹配的pattern，比如/hello, /index.php , /index.aspx等等
- handler 实际响应该pattern的函数

返回值

- 无

函数功能 

- 该函数在缺省的服务器路由（DefaultServeMux）中注册一个函数。当一个请求request进来的时候，缺省的服务器路由会依次根据ServeMux.m中的string（路由表达式）来一个一个匹配。文档（服务器路由）ServeMux解释了路由表达式是如何被匹配的。

例子

    package main
	
	import (
		_ "io"
		"log"
		"net/http"
	)
	
	func HelloServer(w http.ResponseWriter, req *http.Request) {
		// 输出用户自定义错误
		http.Error(w, "this is a error", 404)
	}
	
	func main() {
		// 指定当用户访问 http://www.xxx.com:mmmm/hello 的时候(注意，请不要在hello后面加上/变成hello/)
		// 调用HelloServer这个函数来处理
		http.HandleFunc("/hello", HelloServer)
	
		// 如果顺利的话，你的浏览器会输出 this is a error，并且状态码为404
		err := http.ListenAndServe(":8888", nil)
		if err != nil {
			log.Fatal("ListenAndServe: ", err)
		}
	}

## func ListenAndServe(addr string, handler Handler) error 

参数

- addr http服务监听的地址(端口号)，一般网站默认为80端口
- handler 


返回值

- error 返回错误。一般是端口被占用比较多

函数功能 

- 该函数监听addr指定的端口号，然后调用handler提供的服务处理连接的请求。
handler一般我们可以设置为nil，这样我们会使用缺省的服务路由器。

## func ListenAndServeTLS(addr string, certFile string, keyFile string, handler Handler) error 

参数

- addr http服务监听的地址(端口号)，一般网站默认为80端口
- certFile https 证书文件
- keyFile https key文件
- handler 处理连接请求的函数


返回值

- error 返回错误。一般是端口被占用比较多

函数功能 

- 这个函数基本上跟该函数ListenAndServe功能相同。不过它特别处理https连接。该函数监听addr指定的端口号，然后调用handler提供的服务处理连接的请求。
handler一般我们可以设置为nil，这样我们会使用缺省的服务路由器。特别的，我们必须指定一个证书文件和对应的key文件.单单作为测试，这两个文件我们可以通过Go\src\pkg\crypto\tls\generate_cert.go生成两个文件，放到.exe的目录所在即可。


## func MaxBytesReader(w ResponseWriter, r io.ReadCloser, n int64) io.ReadCloser 

参数

- w ResponseWriter
- r io.ReadCloser，一般可以指向req.Body
- n 限制的大小

返回值

- io.ReadCloser 

函数功能 

- MaxBytesReader跟io.LimitReader函数很像。但是它被设计来设置接收的请求体的最大大小。
跟io.LimitReader不同MaxBytesReader的返回值是一个ReadCloser，当读取超过限制时会返回non-EOF错误。
并且当它调用关闭方法的时候会把潜在的读取者（函数/进程）也关闭掉。

MaxBytesReader用来保护服务器端，以避免客户端偶然或者恶意发送的长数据请求导致的server资源的浪费。 


例子 服务器端
调用这个函数限制客户端上传数据为10个字节

  package main
	
	import (
		"fmt"
		"io"
		"io/ioutil"
		"log"
		"net/http"
	)
	
	// hello world, the web server
	func HelloServer(w http.ResponseWriter, req *http.Request) {
		fmt.Println("come on")
	
		req.Body = http.MaxBytesReader(w, req.Body, 10)
		n, err := io.Copy(ioutil.Discard, req.Body)
		if err == nil {
			fmt.Println("iocpy err")
		}
		if n != 20 {
			fmt.Println("io.Copy = ", n, ", want 20")
		}
	
		io.WriteString(w, "hello, world!hello, world!hello, world!hello, world!hello, world!\n")
	
	}
	
	func main() {
	
		// 指定当用户访问 http://www.xxx.com:mmmm/hello 的时候(注意，请不要在hello后面加上/变成hello/)
		// 调用HelloServer这个函数来处理
		http.HandleFunc("/hello", HelloServer)
	
		err := http.ListenAndServe(":8888", nil)
		if err != nil {
			log.Fatal("ListenAndServe: ", err)
		}
	
	}


客户端发送JSON数据

	package main
	
	import (
		"fmt"
		"net/http"
		"strings"
	)
	
	func main() {
		json := `{"content":"hello,world"}`
		b := strings.NewReader(json)
	
		http.Post("http://localhost:8888/hello", "image/jpeg", b)
		fmt.Println("post ok")
	}


## func NotFound(w ResponseWriter, r *Request) 

参数

- w 响应的写入器
- r 用户请求

返回值

- 无

函数功能 

- 该函数通过一个ResponseWriter对象输出404 page not found。

例子
  package main
	
	import (
		_ "io"
		"log"
		"net/http"
	)
	
	func HelloServer(w http.ResponseWriter, req *http.Request) {
		http.NotFound(w, req)
	}
	
	func main() {
	
		http.HandleFunc("/hello", HelloServer)
		err := http.ListenAndServe(":8888", nil)
		if err != nil {
			log.Fatal("ListenAndServe: ", err)
		}
	}

## func ParseHTTPVersion(vers string) (major, minor int, ok bool) 

参数

- vers 响应的写入器
- r 用户请求

返回值

- major 主版本号
- minor 从版本号
- ok    true或者false

函数功能 

- 该函数解析一个HTTP 版本字符串. 比如输入"HTTP/1.0" 将会返回 (1, 0, true). 

例子
  package main
	
	import (
		"fmt"
		"net/http"
	)
	
	func main() {
		major, minor, ok := http.ParseHTTPVersion("HTTP/1.0")
		fmt.Println(major, minor, ok)
	}

## func ParseTime(text string) (t time.Time, err error) 

参数

- text 日期时间

返回值

- t time.time格式时间
- err 解析错误

函数功能 

- ParseTime解析时间header（例如Date：标头），尝试使用HTTP / 1.1允许的三种格式：TimeFormat，time.RFC850和time.ANSIC。

## func ProxyFromEnvironment(req *Request) (*url.URL, error)

参数列表

- req 用户的请求

返回值：

- *url.URL 代理的URL,如果没有使用代理或者代理全局变量没有定义则返回nil
- error 错误，如果没有使用代理或者代理全局变量没有定义则返回nil

功能说明：
ProxyFromEnvironment返回给定request的代理url.
一般该URL由用户的环境变量$HTTP_PROXY和$NO_PROXY (或$http_proxy和$no_proxy)指定。
如果用户的全局代理环境无效则返回一个错误。
如果用户没有使用代理或者全局环境变量没有定义则会返回一个nil的URL和一个nil的错误。


代码实例

  package main
	
	import (
		"io"
		"log"
		"net/http"
	)
	
	func HelloServer(w http.ResponseWriter, req *http.Request) {
		io.WriteString(w, "<html>\n<body>\n")
		io.WriteString(w, "hello, world!<br/>\n")
	
		myurl, _ := http.ProxyFromEnvironment(req)
		if myurl != nil {
			io.WriteString(w, myurl.Scheme+"<br/>\n")
			io.WriteString(w, myurl.Opaque+"<br/>\n")
			io.WriteString(w, myurl.Host+"<br/>\n")
			io.WriteString(w, myurl.Path+"<br/>\n")
			io.WriteString(w, myurl.RawQuery+"<br/>\n")
			io.WriteString(w, myurl.Fragment+"<br/>\n")
		} else {
			io.WriteString(w, "url is null <br/>\n")
		}
		io.WriteString(w, "</body>\n</html>\n")
	
	}
	
	func main() {
	
		http.HandleFunc("/hello", HelloServer)
	
		err := http.ListenAndServe(":8888", nil)
		if err != nil {
			log.Fatal("ListenAndServe: ", err)
		}
	}


## func ProxyURL(fixedURL *url.URL) func(*Request) (*url.URL, error)

参数列表

- fixedURL 代理的URL

返回值：

- func(*Request) (*url.URL, error) 返回一个代理函数

功能说明：
ProxyURL返回一个代理函数，这个代理函数（一般在Transport中使用）接受请求，并总是返回一个（代理后的）地址。

## func Redirect(w ResponseWriter, r *Request, urlStr string, code int) 

参数列表

- w 服务器响应
- r 客户端请求
- urlStr 要重定向的地址
- code 定义在http里面，一般我们可以使用http.StatusFound

返回值：

- 无

功能说明：
Redirect告诉request重定向到一个url,这个URL可以是请求路径的的相对路径。

代码实例

  package main
	
	import (
		"io"
		"log"
		"net/http"
	)
	
	func HelloServer(w http.ResponseWriter, req *http.Request) {
	
		http.Redirect(w, req, "world", http.StatusFound)
	
	}
	
	func WorldServer(w http.ResponseWriter, req *http.Request) {
		io.WriteString(w, "world server")
	
	}
	
	func main() {
	
		http.HandleFunc("/hello", HelloServer)
		http.HandleFunc("/world", WorldServer)
	
		err := http.ListenAndServe(":9999", nil)
		if err != nil {
			log.Fatal("ListenAndServe: ", err)
		}
	}

## func Serve(l net.Listener, handler Handler) error

参数列表

- l 监听者
- handler Handler参数一般是nil，此时使用DefaultServeMux。

返回值：

- error 成功为nil

功能说明：
Serve接受Listener l接收到的HTTP连接，并为每个连接创建一个新的线程。服务线程会读取每一个请求，调用handler做出回应。Handler参数一般是nil，此时使用DefaultServeMux。

代码实例

  package main
	
	import (
		"io"
		"log"
		"net"
		"net/http"
	)
	
	func HelloServer(w http.ResponseWriter, req *http.Request) {
	
		io.WriteString(w, "hellWorld server")
	
	}
	
	func main() {
	
		http.HandleFunc("/hello", HelloServer)
	
		// 首先，创建用tcp协议监听8888端口
		l, e := net.Listen("tcp", ":8888")
		if e != nil {
			log.Fatal("Listen: ", e)
		}
	
		// 然后在监听的这个端口上启用http服务进行http服务
		err := http.Serve(l, nil)
		if err != nil {
			log.Fatal("Serve: ", err)
		}
	}


## func ServeContent(w ResponseWriter, req *Request, name string, modtime time.Time, content io.ReadSeeker) 

参数列表

- w 服务器响应
- req 客户端请求
- name 文件的名称
- modtime 文件的修改时间 
- content 文件的内容，必须实现io.ReadSeeker这个接口中的方法

返回值：

- error 成功为nil

功能说明：

ServeContent使用ReadSeeker所读取的内容回复给用户请求.
ServeContent比io.Copy更好的是，他能够合适的处理一批请求，设置MIME类型，并且能够处理文件是否修改的请求。
如果响应的内容类型头没有设置,该函数首先会尝试从文件的文件扩展名推断文件类型。
如果推断不出来，则会读取文件的第一个块并传送给DetectContentType来检测类型。
文件名称也可以不使用。
如果文字名称为空，则服务器不会传送给响应。
如果修改时间不为0，ServeContent会把它放在服务器响应的Last-Modified头里面。
如果客户端请求中包含了If-Modified-Since头，ServeContent会使用modtime来判断是否把内容传给客户端。


content的Seek方法必须能够工作。
ServeContent通过定位到文件结尾来确定文件大小。
*os.File中实现了io.ReadSeeker接口。

代码实例

  package main
	
	import (
		"fmt"
		"log"
		"net/http"
		"time"
	)
	
	// 实现一个byte的ReadSeeker
	type MySeeker []byte
	
	// 仅仅是copy输出
	func (d MySeeker) Read(p []byte) (n int, err error) {
		n = copy(p, d)
		fmt.Printf("read is", n)
		return n, nil
	}
	func (d MySeeker) Seek(offset int64, whence int) (ret int64, err error) {
		ret = int64(len(d))
		fmt.Printf("ret is", ret)
		return ret, nil
	}
	
	func Handler(w http.ResponseWriter, r *http.Request) {
		// 仅仅向客户端输出几个字节
		var seeker MySeeker = []byte{'H', 'E', 'L', 'L', 'O', 0}
		
		// 文件名称随便填写了1个
		http.ServeContent(w, r, "1.txt", time.Now(), seeker)
	}
	func main() {
		http.HandleFunc("/hello", Handler)
	
		s := &http.Server{
			Addr: ":8888",
		}
		log.Fatal(s.ListenAndServe())
	}
	
## func ServeFile(w ResponseWriter, r *Request, name string) 

参数列表

- w 响应
- r 客户端请求
- name 文件名或者文件目录名称

返回值：

- 无

功能说明：
该函数实现了向客户请求输出目录或者文件内容。

代码实例

  package main
	
	import (
		"log"
		"net"
		"net/http"
	)
	
	func HelloServer(w http.ResponseWriter, req *http.Request) {
	
		http.ServeFile(w, req, "index.html")
	
	}
	
	func main() {
	
		http.HandleFunc("/hello", HelloServer)
	
		l, e := net.Listen("tcp", ":8888")
		if e != nil {
			log.Fatal("Listen: ", e)
		}
	
		err := http.Serve(l, nil)
		if err != nil {
			log.Fatal("Serve: ", err)
		}
	}

## func SetCookie(w ResponseWriter, cookie *Cookie) 

参数列表

- w 对客户端的响应
- cookie cookie的内容

返回值：

- 无

功能说明：

该函数添加一个Set-Cookie头到客户端响应中


代码实例

  package main
	
	import (
		"log"
		"net"
		"net/http"
		"time"
	)
	
	func HelloServer(w http.ResponseWriter, req *http.Request) {
		expire := time.Now().AddDate(0, 0, 1)
		mycookie := http.Cookie{"test", "testcookie", "/", "www.sanguohelp.com", expire, expire.Format(time.UnixDate),
			86400, true, true, "test=testcookie", []string{"test=tcookie"}}
	
		http.SetCookie(w, &mycookie)
	
	}
	
	func main() {
	
		http.HandleFunc("/hello", HelloServer)
	
		l, e := net.Listen("tcp", ":8888")
		if e != nil {
			log.Fatal("Listen: ", e)
		}
	
		err := http.Serve(l, nil)
		if err != nil {
			log.Fatal("Serve: ", err)
		}
	}

## func StatusText(code int) string 

参数列表

- code 状态码

返回值：

- string 对应状态码的字符串

功能说明：
该函数为一个http状态码返回对应的文本。
如果状态码未知的话，则返回一个空的字符串。

代码实例

  package main
	
	import (
		"fmt"
		"net/http"
	)
	
	func main() {
		fmt.Println(http.StatusText(404))
		fmt.Println(http.StatusText(202))
	}


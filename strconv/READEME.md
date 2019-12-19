# func AppendBool(dst []byte, b bool) []byte

参数列表

- dst 表示原列表 
- b   表示需要添加的bool值，true或者false

返回值：

- []byte  返回原列表追加bool后新生成的列表 

功能说明：

- 将布尔值 b 转换为字符串 "true" 或 "false" 然后将结果追加到 dst 的尾部，返回追加后的 []byte

代码实例：

	type appendBoolTest struct {
	    b   bool
	    in  []byte
	    out []byte
    }
    
    var appendBoolTests = []appendBoolTest{
	    {true, []byte("foo "), []byte("foo true")},
	    {false, []byte("foo "), []byte("foo false")},
    }
    
    func TestAppendBool(t *testing.T) {
	    for _, test := range appendBoolTests {
		    b := AppendBool(test.in, test.b)
		    if !bytes.Equal(b, test.out) {
			    t.Errorf("AppendBool(%q, %v): expected %q but got %q", test.in, test.b, test.out, b)
		    }
	    }
    }
    
# func AppendFloat(dst []byte, f float64, fmt byte, prec int, bitSize int) []byte

参数列表

- dst     原列表
- f       需要append到列表的浮点数
- fmt     转换格式 'b' 'e' 'E' 'f' 'g'或'G'
- prec    浮点数精度
- bitSize 32或64，32对应float32，64对应float64

返回值:

- []byte  返回列表

功能说明：

- 将浮点数f转换为字符串值，并将转换结果追加到dst的尾部，返回追加后的[]byte。
- 浮点数格式有'b' (-ddddp±ddd, 二进制指数), 'e' (-d.dddde±dd, 十进制指数), 'E' (-d.ddddE±dd, 十进制指数), 'f' (-ddd.dddd, 无指数), 'g' (大指数时相当于'e', 其他情况时相当于'f'), 'G' (大指数时相当于'E', 其他情况相当于'f').
- 精度用于控制当格式为'e' 'E' 'f' 'g' 'G'时除指数外的数字的个数；对于'e' 'E' 'f'指小数点后位数；对于'g' 'G'则表示总共的位数；如果使用-1，表示不改变数值的最小位数

代码示例：

	package main
	
	import (
		"fmt"
		"strconv"
	)
	
	func main() {
		f := 100.123456789
		fmt.Println(f)
		c := strconv.AppendFloat(make([]byte, 0), f, 'f', 10, 32)
		fmt.Println(string(c))
		c = strconv.AppendFloat(make([]byte, 0), f, 'e', 10, 32)
		fmt.Println(string(c))
		c = strconv.AppendFloat(make([]byte, 0), f, 'f', 10, 64)
		fmt.Println(string(c))
		c = strconv.AppendFloat(make([]byte, 0), f, 'e', 10, 64)
		fmt.Println(string(c))
	}


代码输出：

	100.123456789
	100.1234588623
	1.0012345886e+02
	100.1234567890
	1.0012345679e+02
	
# func AppendInt(dst []byte, i int64, base int) []byte

参数列表

- dst   表示原列表
- i     表示需要添加的int64值
- base  表示进制数 2 <= base <= 36

返回值：

- 返回[]byte 表示原列表添加数值后新生成的列表

功能说明：

- 类似AppendFloat，只能追加int类型，base表示int表示的进制数，返回追加后的 []byte。当进制大于10时，大于10的值将使用小写a-z表示。

代码实例：

    package main

    import (
        "fmt"
        "strconv"
    )

    func main() {
        newlist := strconv.AppendInt(make([]byte, 0), 123000, 10)
        fmt.Println(newlist) //[49 50 51 48 48 48]
        newlist = strconv.AppendInt(make([]byte, 0), 8, 2)
        fmt.Println(newlist) //[49 48 48 48]
    }
    
# func AppendQuote(dst []byte, s string) []byte

参数列表

- dst   原列表
- s     需要append到列表的字符串

返回值:

- []byte  返回列表

功能说明：

- 将字符串s转换为双引号引起来的字符串，并将结果追加到dst的尾部，返回追加后的[]byte。其中的特殊字符将被转换为转义字符

代码示例：

    package main
    
    import (
        "fmt"
        "strconv"
    )
    
    func main() {
        newlist := strconv.AppendQuote(make([]byte, 0), "")
        fmt.Println(string(newlist))
        newlist = strconv.AppendQuote(make([]byte, 0), "abc")
        fmt.Println(string(newlist))
        newlist = strconv.AppendQuote(make([]byte, 0), "中文")
        fmt.Println(string(newlist))
        newlist = strconv.AppendQuote(make([]byte, 0), "	") // \t
        fmt.Println(string(newlist))
    }

代码输出：

    ""
    "abc"
    "中文"
    "\t"
    
# func AppendQuoteRune(dst []byte, r rune) []byte

参数列表

- dst   原列表
- r     需要append到列表的字符

返回值:

- []byte  返回列表

功能说明：

- 将符文s转换为单引号引起来的字符串，并将结果追加到dst的尾部，返回追加后的[]byte。其中的特殊字符将被转换为转义字符

代码示例：

    package main
    
    import (
        "fmt"
        "strconv"
    )
    
    func main() {
        newlist := strconv.AppendQuoteRune(make([]byte, 0), 'a')
        fmt.Println(string(newlist))
        newlist = strconv.AppendQuoteRune(make([]byte, 0), '\'')
        fmt.Println(string(newlist))
        newlist = strconv.AppendQuoteRune(make([]byte, 0), '中')
        fmt.Println(string(newlist))
    }

代码输出：

    'a'
    '\''
    '中'
    
# func AppendQuoteRuneToASCII(dst []byte, r rune) []byte

参数列表

- dst   原列表
- r     需要append到列表的字符

返回值:

- []byte  返回列表

功能说明：

- 将符文s转换为单引号引起来的字符串，非ASCII字符将转换为ASCII，并将结果追加到dst的尾部，返回追加后的[]byte。其中的特殊字符将被转换为转义字符

代码示例：

    package main
    
    import (
        "fmt"
        "strconv"
    )
    
    func main() {
        newlist := strconv.AppendQuoteRune(make([]byte, 0), 'a')
        fmt.Println(newlist)
        newlist = strconv.AppendQuoteRune(make([]byte, 0), '\'')
        fmt.Println(newlist)
        newlist = strconv.AppendQuoteRune(make([]byte, 0), '中')
        fmt.Println(newlist)
        newlist = strconv.AppendQuoteRuneToASCII(make([]byte, 0), 'a')
        fmt.Println(newlist)
        newlist = strconv.AppendQuoteRuneToASCII(make([]byte, 0), '\'')
        fmt.Println(newlist)
        newlist = strconv.AppendQuoteRuneToASCII(make([]byte, 0), '中')
        fmt.Println(newlist)
    }

代码输出：

    [39 97 39]
    [39 92 39 39]
    [39 228 184 173 39]
    [39 97 39]
    [39 92 39 39]
    [39 92 117 52 101 50 100 39]
    
# func AppendUint(dst []byte, i uint64, base int) []byte

参数列表

- dst   原列表
- i     需要追加到列表的unit64值
- base  unit64的进制

返回值:

- []byte  返回列表

功能说明：

- 类似AppendInt，只能追加uint类型，base表示uint表示的进制数，返回追加后的 []byte

代码示例：

    package main
    
    import (
        "fmt"
        "strconv"
    )
    
    func main() {
        newlist := strconv.AppendUint(make([]byte, 0), 10, 2) // 1010
	    fmt.Println(string(newlist))
	    newlist = strconv.AppendUint(make([]byte, 0), 10, 8) // 12
	    fmt.Println(string(newlist))
	    newlist = strconv.AppendUint(make([]byte, 0), 10, 10) // 10
	    fmt.Println(string(newlist))
    }
    
# func Atoi(s string) (i int, err error)

参数列表

- s 表示数字字符串，如“1234” 

返回值：

- i 表示转换后的数值 

功能说明：

- Atoi是函数ParseInt(s, 10, 0)的简写。把字符串格式的数字如“12345”转化为数字12345

代码实例：

	package main
	
	import (
		"fmt"
		"strconv"
	)
	
    func main() {
        fmt.Println(strconv.Atoi("12345"))
        fmt.Println(strconv.Atoi("abcde"))
    }


代码输出：

    12345 <nil>
    0 strconv.ParseInt: parsing "abcde": invalid syntax
    
# func CanBackquote(s string) bool

参数列表

- s 字符串 

返回值：

- i 表示转换后的数值 

功能说明：

- 判断字符串 s 是否可以表示为一个单行的“反引号”字符串， 字符串中不能含有控制字符（除了 \t）和“反引号”字符，否则返回 false

代码实例：

	package main
	
	import (
		"fmt"
		"strconv"
	)
	
    func main() {
        s := strconv.CanBackquote("C:\\Windows\n")
        fmt.Println(s) // false
        s = strconv.CanBackquote("C:\\Windows\r")
        fmt.Println(s) // false
        s = strconv.CanBackquote("C:\\Windows\f")
        fmt.Println(s) // false
        s = strconv.CanBackquote("C:\\Windows\t")
        fmt.Println(s) // true
        s = strconv.CanBackquote("C:\\`Windows`")
        fmt.Println(s) // false
    }


代码输出：

    false
    false
    false
    true
    false
    
# func FormatBool(b bool) string

参数列表

- b 需要被转换的bool值 

返回值：

- 返回string 表示转换后的字符串 

功能说明：

- 将true或false转换为字符串

代码实例：

	package main
	
	import (
		"fmt"
		"strconv"
	)
	
    func main() {
        b := strconv.FormatBool(true)
        fmt.Println(b)
        b = strconv.FormatBool(false)
        fmt.Println(b)
    }


代码输出：

    true
    false
    
# func FormatFloat(f float64, fmt byte, prec, bitSize int) string

参数列表

- f         需要被转换的float64值 
- fmt       转换格式 'b' 'e' 'E' 'f' 'g'或'G'
- prec      浮点数精度
- bitSize   32或64，32对应float32，64对应float64

返回值：

- 返回string 表示转换后的字符串 

功能说明：

- 将浮点数转换为字符串
- 浮点数格式有'b' (-ddddp±ddd, 二进制指数), 'e' (-d.dddde±dd, 十进制指数), 'E' (-d.ddddE±dd, 十进制指数), 'f' (-ddd.dddd, 无指数), 'g' (大指数时相当于'e', 其他情况时相当于'f'), 'G' (大指数时相当于'E', 其他情况相当于'f').
- 精度用于控制当格式为'e' 'E' 'f' 'g' 'G'时除指数外的数字的个数；对于'e' 'E' 'f'指小数点后位数；对于'g' 'G'则表示总共的位数；如果使用-1，表示不改变数值的最小位数

代码实例：

	package main
	
	import (
		"fmt"
		"strconv"
	)
	
    func main() {
        fmt.Println(strconv.FormatFloat(10.1,'b',5,64))
        fmt.Println(strconv.FormatFloat(10.1,'e',5,64))
        fmt.Println(strconv.FormatFloat(10.1,'E',5,64))
        fmt.Println(strconv.FormatFloat(10.1,'f',5,64))
        fmt.Println(strconv.FormatFloat(10.1,'g',5,64))
        fmt.Println(strconv.FormatFloat(100000000.1,'g',5,64))
        fmt.Println(strconv.FormatFloat(10.1,'G',5,64))
        fmt.Println(strconv.FormatFloat(100000000.1,'G',5,64))
        
        
        fmt.Println(strconv.FormatFloat(10.1,'e',-1,64))
        fmt.Println(strconv.FormatFloat(10.00001,'e',-1,64))
    }


代码输出：

    5685794529555251p-49
    1.01000e+01
    1.01000E+01
    10.10000
    10.1
    1e+08
    10.1
    1E+08
    1.01e+01
    1.010001e+01
    
# func FormatInt(i int64, base int) string

参数列表

- i     表示需要被转换为字符串的int64值
- base  表示进制数  2 <= base <= 36

返回值：

- 返回string 表示转换后的字符串，当进制大于10时，大于10的值将使用小写a-z表示。

功能说明：

- 将数值按照进制格式转换为字符串

代码实例：

	package main
	
	import (
		"fmt"
		"strconv"
	)
	
    func main() {
        fmt.Println(strconv.FormatInt(9223372036854775807, 2))
        fmt.Println(strconv.FormatInt(9223372036854775807, 10))
    }


代码输出：

    111111111111111111111111111111111111111111111111111111111111111
    9223372036854775807
    

# func FormatUint(i uint64, base int) string

参数列表

- i     表示需要被转换为字符串的int64值
- base  表示进制数  2 <= base <= 36

返回值：

- 返回string 表示转换后的字符串，当进制大于10时，大于10的值将使用小写a-z表示。

功能说明：

- 将数值按照进制格式转换为字符串

代码实例：

	package main
	
	import (
		"fmt"
		"strconv"
	)
	
    func main() {
        fmt.Println(strconv.FormatUint(18446744073709551615, 2))
        fmt.Println(strconv.FormatUint(18446744073709551615, 10))
    }


代码输出：

    1111111111111111111111111111111111111111111111111111111111111111
    18446744073709551615
    
# func IsPrint(r rune) bool

参数列表

- r     表示rune字符

返回值：

- 返回bool true表示可以打印，false表示不可以打印。

功能说明：

- 判断rune字符在golang中是否被定义为可打印，与unicode.IsPrint相同。可打印范围包括字符、数字、标点、符号以及ASCII中的空格。

代码实例：

	package main
	
	import (
		"fmt"
		"strconv"
	)
	
    func main() {
        fmt.Println(strconv.IsPrint(' '))
        fmt.Println(strconv.IsPrint('\t'))
        fmt.Println(strconv.IsPrint('\n'))
        fmt.Println(strconv.IsPrint('\r'))
    }


代码输出：

    true
    false
    false
    false
    
# func Itoa(i int) string

参数列表

- i     表示需要被转换为字符串的int值

返回值：

- 返回string 表示转换后的字符串。

功能说明：

- 将数值按照10进制转换为字符串,是等同于FormatInt(i, 10)的简写。

代码实例：

	package main
	
	import (
		"fmt"
		"strconv"
	)
	
    func main() {
        fmt.Println(strconv.FormatInt(9223372036854775807, 10))
    }

代码输出：

    9223372036854775807
    
# func (e *NumError) Error() string

返回值：

- 返回string     描述错误的字符串

功能说明：

- 返回描述NumError类型错误的字符串

代码实例：

    package main
    
    import (
        "fmt"
        "strconv"
    )
    
    func main() {
        err := errors.New("too large")
        er := strconv.NumError{Func: "anyfunc", Num: "1e100",Err:err}
        fmt.Println(er.Error())
    }

代码输出：

    strconv.anyfunc: parsing "1e100": too large
    
# func ParseBool(str string) (value bool, err error)

参数列表

- str     可以表示bool值的字符串

返回值：

- value   通过str转换的bool值
- err     当str无法转换为bool返回错误，否则为nil

功能说明：

- 尝试将表示bool值的字符串转换为bool值。str可以是1, t, T, TRUE, true, True, 0, f, F, FALSE, false, False，其他的字符将返回错误。

代码实例：

    package main
    
    import (
        "fmt"
        "strconv"
    )
    
    func main() {
        fmt.Println(strconv.ParseBool("1"))
        fmt.Println(strconv.ParseBool("0"))
        fmt.Println(strconv.ParseBool("a"))
    }

代码输出：

    true <nil>
    false <nil>
    false strconv.ParseBool: parsing "a": invalid syntax
    
# func ParseFloat(s string, bitSize int) (f float64, err error)

参数列表

- str     可以表示float64值的字符串
- bitSize 精度 按64位或32位转换为float64值

返回值：

- f       通过str转换的float64值.如果解析出错，返回0；数值超范围返回±Inf。
- err     当str无法转换为float64值返回错误，否则为nil

功能说明：

- 尝试按照bitSize指定的精度将表示float64值的字符串转换为float64值。当bitSize指定32位时，返回值仍然是float64值而非float32值,但却可以在不改变数值的情况下将float64转换为float32。
- 如果s是一个float格式或接近float格式的字符串，ParseFloat将返回按照IEEE 754规范舍入的float64值。
- 返回的err是*NumError格式，并且err.Num = s
- 如果s格式不是float格式，返回语法错误 err.Err = ErrSyntax。
- 如果s格式正确但转换成浮点数值后比bitSize指定的精度的最大浮点数大1/2 ULP（unit in the last place），返回值 f = ±Inf, err.Err = ErrRange。
代码实例：

    package main
    
    import (
        "fmt"
        "strconv"
    )
    
    func main() {
        fmt.Println(strconv.ParseFloat("1.0231e2",64))
    }

代码输出：

    102.31 <nil>
    
# func ParseInt(s string, base int, bitSize int) (i int64, err error)

参数列表

- str     可以表示int64值的字符串
- base    进制 (2 to 36) 
- bitSize 精度 0、8、16、32、64对应int、int8、int16、int32、int64

返回值：

- i       通过str转换的int64值.
- err     当str无法转换为init64值返回错误，否则为nil.

功能说明：

- 尝试按照base指定的进制(2-36)将表示int64值的字符串转换为int64值。如果base为0,则参考s的格式自动确定进制，如："0x"是16进制，"O"是8进制，其余是10进制。
- 返回err是*NumError格式，并且err.Num = s。如果s格式错误，则err.Err = ErrSyntax，并且i将返回0.如果转换的数值超过bitSize指定的带符号数值（signed integer），i将返回符合该bitSize的最大值符号数值。

代码实例：

    package main
    
    import (
        "fmt"
        "strconv"
    )
    
    func main() {
        fmt.Println(strconv.ParseInt("9223372036854775807",10,64))
        fmt.Println(strconv.ParseInt("9223372036854775808",10,64))
        fmt.Println(strconv.ParseInt("0xa",0,64))
    }

代码输出：

    9223372036854775807 <nil>
    9223372036854775807 strconv.ParseInt: parsing "9223372036854775808": value out of range
    10 <nil>
    
    
# func ParseUint(s string, base int, bitSize int) (n uint64, err error)

参数列表

- str     可以表示int64值的字符串
- base    进制 (2 to 36) 
- bitSize 精度 0、8、16、32、64对应uint、uint8、uint16、uint32、uint64

返回值：

- i       通过str转换的uint64值.
- err     当str无法转换为uinit64值返回错误，否则为nil.

功能说明：

- ParseUint is like [ParseInt](ParseInt.md) but for unsigned numbers.

代码实例：

    package main
    
    import (
        "fmt"
        "strconv"
    )
    
    func main() {
        fmt.Println(strconv.ParseUint("18446744073709551615",10,64))
        fmt.Println(strconv.ParseUint("18446744073709551616",10,64))
        fmt.Println(strconv.ParseUint("0xa",0,64))
    }

代码输出：

    18446744073709551615 <nil>
    18446744073709551615 strconv.ParseUint: parsing "18446744073709551616": value out of range
    10 <nil>
    
    
# func Quote(s string) string

参数列表

- s     被引用的字符串

返回值：

- 返回string 将s转换为被引用的字符串格式

功能说明：

- 对s两侧添加双引号，并对s中的控制字符和不可打印的字符进行转义。

代码实例：

    package main
    
    import (
        "fmt"
        "strconv"
    )
    
    func main() {
        fmt.Println(strconv.Quote("abc	中文"))
        fmt.Println(strconv.Quote(strconv.Quote("abc	中文")))
    }

代码输出：

    "abc\t中文"
    "\"abc\\t中文\""
    
# func QuoteRune(r rune) string

参数列表

- r     被引用的rune字符

返回值：

- 返回string 将r转换为被引用的字符格式

功能说明：

- 对s两侧添加单引号，并对r中的控制字符和不可打印的字符进行转义。

代码实例：

    package main
    
    import (
        "fmt"
        "strconv"
    )
    
    func main() {
        fmt.Println(strconv.QuoteRune('	'))
        fmt.Println(strconv.QuoteRune(100))
    }

代码输出：

    '\t'
    'd'
    
# func QuoteRuneToASCII(r rune) string

参数列表

- r     被引用的rune字符

返回值：

- 返回string 将r转换为被引用的字符格式

功能说明：

- 对s两侧添加单引号，并对r中的非ASCII字符和不可打印的字符进行转义。

代码实例：

    package main
    
    import (
        "fmt"
        "strconv"
    )
    
    func main() {
        fmt.Println(strconv.QuoteRune('中'))
        fmt.Println(strconv.QuoteRuneToASCII('中'))
        fmt.Println(strconv.QuoteRuneToASCII('	'))
    }

代码输出：

    '中'
    '\u4e2d'
    '\t'
    
# func Unquote(s string) (t string, err error)

参数列表

- s     被单引号、双引号或反引号引用的字符串

返回值：

- t     将s转换为被引用前的字符串
- err

功能说明：

- 返回将被（单引号、双引号、反引号）引用的字符串的原字符串。（如果s是被单引号引用，则被引用的字符串必须是go中的字符，并返回该单字符的字符串。）

代码实例：

    package main
    
    import (
        "fmt"
        "strconv"
    )
    
    func main() {
        test := func(s string) {
            t, err := strconv.Unquote(s)
            if err != nil {
                fmt.Printf("Unquote(%#v) error： %v\n", s, err)
            } else {
                fmt.Printf("Unquote(%#v) = %v\n", s, t)
            }
        }
    
        s := `cafe\u0301`
        // If the string doesn't have quotes, it can't be unquoted.
        test(s) // invalid syntax
        test("`" + s + "`")
        test(`"` + s + `"`)
    
        test(`'\u00e9'`)
    
    }

代码输出：

    Unquote("cafe\\u0301") error： invalid syntax
    Unquote("`cafe\\u0301`") = cafe\u0301
    Unquote("\"cafe\\u0301\"") = café
    Unquote("'\\u00e9'") = é
    
# func UnquoteChar(s string, quote byte) (value rune, multibyte bool, tail string, err error)

参数列表

- s         转义后的字符串
- quote     字符串使用的引号符。
    如果设置为单引号，则 s 中允许出现 \' 字符，不允许出现单独的 ' 字符
    如果设置为双引号，则 s 中允许出现 \" 字符，不允许出现单独的 " 字符
    如果设置为 0，则不允许出现 \' 或 \" 字符，可以出现单独的 ' 或 " 字符

返回值：

- value     解码后的字符
- multibyte value是否为多字节字符
- tail      字符串 s 除去 value 后的剩余部分
- err       返回 s 中是否存在语法错误

功能说明：

- 将 s 中的第一个字符“取消转义”并解码


代码实例：

    func main() {
        sr := `\"大\\家\\好！\"`
        var c rune
        var mb bool
        var err error
        for ; len(sr) > 0; c, mb, sr, err = strconv.UnquoteChar(sr, '"') {
            fmt.Println(c, mb,sr,err)
        }
    }

代码输出：

    0 false \"大\\家\\好！\" <nil>
    34 false 大\\家\\好！\" <nil>
    22823 true \\家\\好！\" <nil>
    92 false 家\\好！\" <nil>
    23478 true \\好！\" <nil>
    92 false 好！\" <nil>
    22909 true ！\" <nil>
    65281 true \" <nil>
    

    

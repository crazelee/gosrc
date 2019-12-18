# func Contains(s, substr string) bool

参数列表

- s 表示需要判断的主串 
- substr 需要查询的子串

返回值：

- 返回bool

功能说明：

判断s中是否包含substr子串，包含返回true，否者返回false

代码实例：

	package main
    
    import (
    	"fmt"
    	"strings"
    )
    
    func main() {
    	fmt.Println(strings.Contains("seafood", "foo")) //true
    	fmt.Println(strings.Contains("seafood", "bar")) //false
    	fmt.Println(strings.Contains("seafood", ""))    //true
    	fmt.Println(strings.Contains("", ""))           //true
    }
    
# func ContainsAny(s, chars string) bool

参数列表

- s 表示需要判断的主串 
- chars 表示保存的unicode字符串

返回值：

- 返回bool

功能说明：

这个函数主要是用来判断s中是否包含chars中的字符中的任意字符，如果包含返回true，否者返回false

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Println(strings.ContainsAny("team", "i"))       //false
		fmt.Println(strings.ContainsAny("failure", "wwwi")) //true
		fmt.Println(strings.ContainsAny("foo", ""))         //false
		fmt.Println(strings.ContainsAny("", ""))            //false
	}
	
	
# func ContainsRune(s string, r rune) bool

参数列表

- s 表示需要判断的主串 
- r 表示rune字符

返回值：

- 返回bool

功能说明：

这个函数主要是用来判断s中是否包含rune类型（unicode）的r字符，如果包含返回true，否者返回false

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Println(strings.ContainsRune("team", rune('m')))    //true
		fmt.Println(strings.ContainsRune("failure", rune('w'))) //false
		fmt.Println(strings.ContainsRune("谢foo", rune('谢')))    //true
		fmt.Println(strings.ContainsRune("", 30))               //false
	}

# func Count(s, sep string) int

参数列表

- s 表示需要判断的主串 
- sep 需要计算的子串

返回值：

- 返回int 表示s中包含sep的个数 

功能说明：

这个函数主要是用来判断s中包含了多少个sep

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Println(strings.Count("cheese", "e"))  //3
		fmt.Println(strings.Count("cheese", "ee")) //1
		fmt.Println(strings.Count("five", ""))     // 5
	
	}
	
# func EqualFold(s, t string) bool

参数列表

- s 表示需要判断的主串 
- t 表示需要比较的辅串

返回值：

- 返回bool

功能说明：

字符串s和t比较，它们在全部小写的情况下，采用UTF8编码的底层的unicode是否一致

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Println(strings.EqualFold("Go", "go"))  //true
	}
	
# func Fields(s string) []string

参数列表

- s 表示需要判断的主串

返回值：

- 返回[]string 

功能说明：

s按照一个空格或者多个连续的空格分割，返回分割之后的串数组，如果字符串没有空格或者只有一个空格，那么返回元素为去空格的s字符串

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Printf("Fields are: %q", strings.Fields("  foo bar  baz   ")) //Fields are: ["foo" "bar" "baz"]
		fmt.Printf("Fields are: %q", strings.Fields(" baz ")) //Fields are: ["bar"]
	}
	
# func FieldsFunc(s string, f func(rune) bool) []string

参数列表

- s 表示需要判断的主串
- f 表示一个函数，该函数参数是rune，返回值是bool，如果rune符合f函数的逻辑那么返回true，否者返回false

返回值：

- 返回[]string 

功能说明：

该函数实现的功能：s的每一个字符传入函数f，如果f返回true，那么按照该字符进行分割（该字符不保留），继续下一个字符，以此类推直到最后，如果返回的都是为false或者s为空，那么将返回空的字符串slice

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		a := strings.FieldsFunc("astaxie", splitfunc)
		fmt.Println(a) //输出：[asta ie]
		//如果把下面的函数t字符改成，那么将返回空slice
	}
	
	func splitfunc(a rune) bool {
		if a > 't' {
			return true
		}
		return false
	}

# func HasPrefix(s, prefix string) bool

参数列表

- s 表示需要判断的主串
- prefix 需要判断的前缀字符串

返回值：

- 返回bool，

功能说明：

该函数主要判断s串中是否含有前缀prefix，如果包含，那么返回true，否则返回false

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Println(strings.HasPrefix("astaxie", "as")) //true
		fmt.Println(strings.HasPrefix("astaxie", "ta")) //false
	}
	
# func HasSuffix(s, suffix string) bool

参数列表

- s 表示需要判断的主串
- suffix 需要判断的后缀字符串

返回值：

- 返回bool，

功能说明：

该函数主要判断s串中是否含有后缀suffix，如果包含，那么返回true，否则返回false

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Println(strings.HasSuffix("astaxie", "as")) //false
		fmt.Println(strings.HasSuffix("astaxie", "xie")) //true
	}
	
# func Index(s, sep string) int

参数列表

- s 表示需要判断的主串
- sep 需要判断的第一次出现位置的字符串

返回值：

- 返回int，对应sep出现在s中的位置

功能说明：

该函数主要判断sep串在s串中第一次出现的位置，如果不存在返回-1

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Println(strings.Index("chickenkenken", "ken"))  //4
		fmt.Println(strings.Index("chicken", "dmr"))        //-1
	}
	
# func IndexAny(s, chars string) int

参数列表

- s 表示需要判断的主串
- chars 需要判断的第一次出现位置的字符集

返回值：

- 返回int，对应sep出现在s中的位置

功能说明：

该函数主要判断chars集中任意的一个字符在s串中第一次出现的位置，如果不存在返回-1

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Println(strings.IndexAny("chickenkenkenken", "iken"))   //2
		fmt.Println(strings.IndexAny("chicken", "dmr"))   //-1
	}
	
# func IndexFunc(s string, f func(rune) bool) int

参数列表

- s 表示需要判断的主串
- f 表示一个函数，该函数参数是rune，返回值是bool，如果rune符合f函数的逻辑那么返回true，否者返回false

返回值：

- 返回int，对应符合函数f的字符的位置

功能说明：

该函数主要判断s中的每一个字符传入函数f，如果符合，那么返回该字符的位置，如果都不符合则返回-1

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Println(strings. IndexFunc("astaxie", splitfunc))  //符合条件的是字符x，因为字符x的rune大于t，所以这个位置应该返回4
		fmt.Println(strings. IndexFunc("aaabbbb", splitfunc))  //所有的字符都不符合条件，则返回-1
	}
	
	func splitfunc(a rune) bool {
		if a > 't' {
			return true
		}
		return false
	}
	
# func IndexRune(s string, r rune) int

参数列表

- s 表示需要判断的主串
- r 需要判断的第一次出现位置的unicode码
返回值：

- 返回int，对应r出现在s中的位置

功能说明：

该函数主要判断unicode r在s串中第一次出现的位置，如果不存在返回-1

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Println(strings.IndexRune("chicken", 'k'))  //4
		fmt.Println(strings.IndexRune("chicken", 'd'))  //-1
	}
	
# func Join(a []string, sep string) string

参数列表

- a 表示需要链接起来的字符串slice
- sep 表示链接的符号

返回值：

- 返回string

功能说明：

该函数主要实现字符串slice的链接功能，把slice的每一个元素通过sep进行链接

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		s := []string{"foo", "bar", "baz"}
		fmt.Println(strings.Join(s, ", ")) //foo, bar, baz
	}
	
# func LastIndex(s, sep string) int

参数列表

- s 表示需要判断的对象字符串
- sep 表示最后出现的字符串

返回值：

- 返回int

功能说明：

该函数主要判断sep串在s串中最后一次出现的位置，如果不存在返回-1 

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Println(strings.LastIndex("chickenkenken", "ken"))  //10
		fmt.Println(strings.LastIndex("chicken", "dmr"))        //-1
	}
	
# func LastIndexAny(s, chars string) int

参数列表

- s 表示需要判断的主串
- chars 需要判断的最后一次出现位置的字符集

返回值：

- 返回int，对应sep出现在s中的最后位置

功能说明：

该函数主要判断chars集中任意的一个字符在s串中最后一次出现的位置，如果不存在返回-1

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Println(strings.LastIndexAny("chickenkenkenken", "iken"))   //15
		fmt.Println(strings.LastIndexAny("chicken", "dmr"))   //-1
	}
	
# func LastIndexFunc(s string, f func(rune) bool) int

参数列表

- s 表示需要判断的主串
- f 表示一个函数，该函数参数是rune，返回值是bool，如果rune符合f函数的逻辑那么返回true，否者返回false

返回值：

- 返回int，对应符合函数f的字符的位置

功能说明：

该函数主要判断s中的每一个字符传入函数f，返回符合函数f的最后一个字符的位置，如果都不符合则返回-1

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Println(strings.LastIndexFunc("astaxie", splitfunc)) //符合条件的有字符t和x，因为字符x是最后出现的位置，所以这个位置应该返回4
		fmt.Println(strings.LastIndexFunc("aaabbbb", splitfunc)) //所有的字符都不符合条件，则返回-1
	}
	
	func splitfunc(a rune) bool {
		if a > 'm' {
			return true
		}
		return false
	}
	
# func Map(mapping func(rune) rune, s string) string

参数列表

- mapping 处理函数，输入是字符，输出是字符
- s 表示需要处理的主串

返回值：

- 返回string，处理后的字符串

功能说明：

该函数以此读取s中的字符，传入mapping函数，然后返回的字符链接起来，说白了就是字符串的每一个字符通过mapping函数的处理，最后返回处理好的字符串，如果处理不正确，那么就抛弃该字符

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		rot13 := func(r rune) rune {
			switch {
			case r >= 'A' && r <= 'Z':
				return 'A' + (r-'A'+13)%26
			case r >= 'a' && r <= 'z':
				return 'a' + (r-'a'+13)%26
			}
			return r
		}
		fmt.Println(strings.Map(rot13, "'Twas brillig and the slithy gopher..."))
		//'Gjnf oevyyvt naq gur fyvgul tbcure...
	}
	
# type Reader
 Reader是通过读取一个字符串之后实现了io.Reader, io.ReaderAt, io.Seeker, io.ByteScanner, 和io.RuneScanner 接口

## func NewReader(s string) *Reader
参数列表

- s 读取的字符串

返回值：

- *Reader 通过读取一个字符串之后返回Reader对象

对象的方法列表：

- func (r *Reader) Len() int   //返回未读取的字符串的长度
- func (r *Reader) Read(b []byte) (n int, err error)  //读取数据到b中，返回读取的实际大小n，如果出错返回err，例如EOF或者b的长度为0
- func (r *Reader) ReadAt(b []byte, off int64) (n int, err error) //按照指定的off位置开始读取内容到b，返回读取的实际大小n，如果出错返回err，例如off小于0或者大于本身的长度或者文件尾
- func (r *Reader) ReadByte() (b byte, err error)  //读取一个byte的数据
- func (r *Reader) ReadRune() (ch rune, size int, err error)  //读取一个rune的数据
- func (r *Reader) Seek(offset int64, whence int) (int64, error) //根据whence来移动offset，如果whence=0为直接移动offset位置，=1为移动到当前位置之后的offset，=2为移动到当前字符串长度之后的offset位置
- func (r *Reader) UnreadByte() error  //当前读取的位置向前移一个byte
- func (r *Reader) UnreadRune() error  //当前读取的位置向前移一个rune

功能说明：

该函数主要是通过把字符串读取Reader之后进行的一些读取操作

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		read := strings.NewReader("I am asta谢")
		var b []byte
		fmt.Println(read.Len())  //12
		b = make([]byte,8)
		n, err := read.Read(b)
		if err != nil {
			fmt.Println(err)
		}
		fmt.Println(b)   //[73 32 97 109 32 97 115 116]
		fmt.Println(n)   //8
		n, err = read.ReadAt(b,3)
		if err != nil {
			fmt.Println(err)
		}
		fmt.Println(b)   //[109 32 97 115 116 97 232 176]
		fmt.Println(n)   //8
		bt,err:=read.ReadByte()	
		if err != nil {
			fmt.Println(err)
		}
		fmt.Println(bt)  //97
		rn,size,err:=read.ReadRune()	
		if err != nil {
			fmt.Println(err)
		}
		fmt.Println(rn)    //35874
		fmt.Println(size)  //3
	}


# type Replacer
这是一个字符串替换的对象

## func NewReplacer(oldnew ...string) *Replacer

参数列表

- oldnew是一个slice，是一个需要替换的字符串和新的字符串的配对出现

返回参数

- Replacer返回一个替换对象

Replacer方法列表

- func (r *Replacer) Replace(s string) string   // 把字符串替换为oldnew定义的
- func (r *Replacer) WriteString(w io.Writer, s string) (n int, err error)  //替换之后的字符串写入到w之中，返回写入的数量

应用示例，下面代码来自于beego的模板替换：

	package main

	import (
		"fmt"
		"strings"
		"os"
	)
	
	func main() {
		patterns := []string{"abc", "efg"}
		replacer := strings.NewReplacer(patterns...)
		format := replacer.Replace("abc is abc is abc")
		fmt.Println(format)
		//efg is efg is efg
		replacer.WriteString(os.Stdout,"abc is abc is abc")
		//efg is efg is efg
	}
    
# func Repeat(s string, count int) string

参数列表

- s 表示需要重复的字符串
- count 表示重复字数

返回值：

- 返回string 重复的字符串

功能说明：

该函数返回一个s的重复count字数的字符串

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Println("ba" + strings.Repeat("na", 2))  //banana
	}
	
# func Replace(s, old, new string, n int) string

参数列表

- s 表示需要替换的主字符串
- old 表示需要替换的字符串
- new 表示替换的新字符串
- n 表示替换的次数

返回值：

- 返回string，处理之后的字符串

功能说明：

该函数实现在s中把old替换为new字符串，替换次数为n，如果n小于0，那么就全部替换

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Println(strings.Replace("oink oink oink", "k", "ky", 2))   //oinky oinky oink
		fmt.Println(strings.Replace("oink oink oink", "oink", "moo", -1))   //moo moo moo
	}
	
# func Split(s, sep string) []string

参数列表

- s 表示需要处理的字符串
- sep 表示分割的字符串

返回值：

- 返回[]string 分割之后的字符串slice

功能说明：

该函数s根据sep分割，返回分割之后子字符串的slice，如果sep为空，那么每一个字符都分割

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Printf("%q\n", strings.Split("a,b,c", ","))   //["a" "b" "c"]
		fmt.Printf("%q\n", strings.Split("a man a plan a canal panama", "a "))  //["" "man " "plan " "canal panama"]
		fmt.Printf("%q\n", strings.Split(" xyz ", ""))  //[" " "x" "y" "z" " "]
		fmt.Printf("%q\n", strings.Split("", "Bernardo O'Higgins"))   //[""]
	}
	
# func SplitAfter(s, sep string) []string

参数列表

- s 表示需要处理的字符串
- sep 表示分割的字符串

返回值：

- 返回[]string 分割之后的字符串slice

功能说明：

该函数s根据sep分割，返回分割之后子字符串的slice,和split一样，只是返回的子字符串保留sep，如果sep为空，那么每一个字符都分割

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Printf("%q\n", strings.SplitAfter("a,b,c", ","))  //["a," "b," "c"]
	}


# func SplitAfterN(s, sep string, n int) []string

参数列表

- s 表示需要处理的字符串
- sep 表示分割的字符串
- n 表示需要分割的子字符串

	- n > 0: 最多n个子字符串; 最后一个就是剩下未分割的子字符串.
	- n == 0: 返回为0的字符串
	- n < 0: 返回所有的子字符串，和SplitAfter

返回值：

- 返回[]string 分割之后的字符串slice

功能说明：

该函数s根据sep分割，返回分割之后子字符串的slice,和split一样，只是返回的子字符串保留sep，如果sep为空，那么每一个字符都分割

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Printf("%q\n", strings.SplitAfterN("a,b,c", ",", 2))  //["a," "b,c"]
		fmt.Printf("%q\n", strings.SplitAfterN("a,b,c", "", 5))   //["a" "," "b" "," "c"]
		fmt.Printf("%q\n", strings.SplitAfterN("a,b,c", ",", 1))   //["a,b,c"]
	}
	
# func SplitN(s, sep string, n int) []string

参数列表

- s 表示需要处理的字符串
- sep 表示分割的字符串
- n 表示分割的最多子串

	- n > 0: 最多n个子字符串; 最后一个就是剩下未分割的子字符串.
	- n == 0: 返回为0的字符串
	- n < 0: 返回所有的子字符串，和SplitAfter

返回值：

- 返回[]string 分割之后的字符串slice

功能说明：

该函数s根据sep分割，返回分割之后子字符串的slice，返回的子串的长度如n的定义，如果sep为空，那么每一个字符都分割

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Printf("%q\n", strings.SplitN("a,b,c", ",", 2))  //["a" "b,c"]
		z := strings.SplitN("a,b,c", ",", 0)
		fmt.Printf("%q (nil = %v)\n", z, z == nil)  //[] (nil = true)
	}


# func Title(s string) string

参数列表

- s 表示需要处理的字符串

返回值：

- 返回string 转化之后的字符串

功能说明：

该函数把s字符串里面的每个单词首字母转化为大写

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Println(strings.Title("her royal highness"))
		//Her Royal Highness
	}

# func ToLower(s string) string

参数列表

- s 表示需要处理的字符串

返回值：

- 返回string 转化之后的字符串

功能说明：

该函数把s字符串里面的每个单词转化为小写

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Println(strings.ToLower("Gopher"))
		//gopher
	}
	
# func ToLowerSpecial(_case unicode.SpecialCase, s string) string

参数列表

- _case 表示unicode的SpecialCase对象
- s 表示需要处理的字符串

返回值：

- 返回string 转化之后的字符串

功能说明：

该函数把s字符串里面的每个单词转化为小写，但是调用的是unicode.SpecialCase的ToLower方法

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
		"unicode"
	)
	
	func main() {
		var SC unicode.SpecialCase
		fmt.Println(strings.ToLowerSpecial(SC, "Gopher"))
		//gopher
	}
	
# func ToTitle(s string) string

参数列表

- s 表示需要处理的字符串

返回值：

- 返回string 转化之后的字符串

功能说明：

该函数把s字符串里面的每个字符转化为对应的大写字符，其实和ToUpper一样的效果，但是有些语种的unicode,ToTitle和ToUpper效果不一样，但是我没试出来过，英语至少是一样的。

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Println(strings.ToTitle("Gopher"))
		//GOPHER
	}
	
# func ToTitleSpecial(_case unicode.SpecialCase, s string) string

参数列表

- _case 表示unicode的SpecialCase对象
- s 表示需要处理的字符串

返回值：

- 返回string 转化之后的字符串

功能说明：

该函数把s字符串里面的每个单词转化为标题体，但是调用的是unicode.SpecialCase的ToTitle方法

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
		"unicode"
	)
	
	func main() {
		var SC unicode.SpecialCase
		fmt.Println(strings.ToTitleSpecial(SC, "Gopher"))
		//GOPHER
	}
	
# func ToUpper(s string) string

参数列表

- s 表示需要处理的字符串

返回值：

- 返回string 转化之后的字符串

功能说明：

该函数把s字符串里面的每个字符转化为大写

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Println(strings.ToUpper("Gopher"))
		//GOPHER
	}
	
# func ToUpperSpecial(_case unicode.SpecialCase, s string) string

参数列表

- _case 表示unicode的SpecialCase对象
- s 表示需要处理的字符串

返回值：

- 返回string 转化之后的字符串

功能说明：

该函数把s字符串里面的每个单词转化为大写，但是调用的是unicode.SpecialCase的ToUpper方法

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
		"unicode"
	)
	
	func main() {
		var SC unicode.SpecialCase
		fmt.Println(strings.ToUpperSpecial(SC, "Gopher"))
		//GOPHER
	}
	
# func Trim(s string, cutset string) string

参数列表

- s 表示需要处理的字符串
- cutset 表示需要过滤的字符集

返回值：

- 返回string 转化之后的字符串

功能说明：

该函数把s字符串开头或者结尾里面包含字符集的字符全部过滤掉，返回过滤之后的字符串

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Printf("[%q]", strings.Trim(" !!! Achtung !!! ", "! "))
		//["Achtung"]
	}
	
# func TrimFunc(s string, f func(rune) bool) string

参数列表

- s 表示需要处理的字符串
- f 表示一个函数，判断是否过滤该字符的函数，如果为真那么就过滤

返回值：

- 返回string 转化之后的字符串

功能说明：

该函数把s字符串里面开头和结尾部分字符传入f函数进行判断是否过滤，为真就过滤

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Printf("[%q]", strings.TrimFunc("xxastaxieyy", filte))
		//astaxie
	}
	
	func filte(r rune) bool {
		if r > 't' {
			return true
		}
		return false
	}
	
# func TrimLeft(s string, cutset string) string

参数列表

- s 表示需要处理的字符串
- cutset 表示需要过滤的字符集

返回值：

- 返回string 转化之后的字符串

功能说明：

该函数把s字符串开头里面包含字符集的字符全部过滤掉，返回过滤之后的字符串

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Printf("[%q]", strings.TrimLeft(" !!! Achtung !!! ", "! "))
		//["Achtung !!! "]
	}
	
# func TrimLeftFunc(s string, f func(rune) bool) string

参数列表

- s 表示需要处理的字符串
- f 表示一个函数，判断是否过滤该字符的函数，如果为真那么就过滤

返回值：

- 返回string 转化之后的字符串

功能说明：

该函数把s字符串里面开头部分字符传入f函数进行判断是否过滤，为真就过滤

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Printf("[%q]", strings.TrimLeftFunc("xxastaxieyy", filte))
		//astaxieyy
	}
	
	func filte(r rune) bool {
		if r > 't' {
			return true
		}
		return false
	}
	
# func TrimRight(s string, cutset string) string

参数列表

- s 表示需要处理的字符串
- cutset 表示需要过滤的字符集

返回值：

- 返回string 转化之后的字符串

功能说明：

该函数把s字符串结尾里面包含字符集的字符全部过滤掉，返回过滤之后的字符串

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Printf("[%q]", strings.TrimRight(" !!! Achtung !!! ", "! "))
		//[" !!! Achtung"]
	}
	
# func TrimRightFunc(s string, f func(rune) bool) string

参数列表

- s 表示需要处理的字符串
- f 表示一个函数，判断是否过滤该字符的函数，如果为真那么就过滤

返回值：

- 返回string 转化之后的字符串

功能说明：

该函数把s字符串里面结尾部分字符传入f函数进行判断是否过滤，为真就过滤

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Printf("[%q]", strings.TrimRightFunc("xxastaxieyy", filte))
		//xxastaxie
	}
	
	func filte(r rune) bool {
		if r > 't' {
			return true
		}
		return false
	}
	
# func TrimSpace(s string) string

参数列表

- s 表示需要处理的字符串

返回值：

- 返回string 转化之后的字符串

功能说明：

该函数把s字符串开头或者结尾里面空白符('\t', '\n', '\v', '\f', '\r', ' ', U+0085 (NEL), U+00A0 (NBSP))全部过滤掉，返回过滤之后的字符串

代码实例：

	package main
	
	import (
		"fmt"
		"strings"
	)
	
	func main() {
		fmt.Println(strings.TrimSpace(" \t\n a lone gopher \n\t\r\n"))
		//a lone gopher
	}
	

# 什么是 GO 语言

* ##### Google 开源

* ##### 编译型语言

* ##### 21世纪的 C 语言

---

# Go 语言的特点

* ##### 语法简洁

* ##### 开发效率高

* ##### 执行性能好

* ##### 天生支持并发

* ##### 自带格式化

# Go语言开发环境搭建

## 安装Go开发包

## 下载

[https://golang.google.cn/dl/]()

![image-20200610212700688](C:\Users\RHW\AppData\Roaming\Typora\typora-user-images\image-20200610212700688.png)

##### 注意：建议安装路径不要太过复杂

# 配置GOPATH

#### 详细步骤

1. 在自己的电脑上新建一个目录`D:\go`（存放我编写的Go语言代码）
2. 在环境变量里，新建一项：`GOPATH:D:\`
3. 在`D:\go`下新建三个文件夹，分别是：`bin`、`pkg`、`src`
4. 把`D:\go\bin`这个目录添加到到 PATH 环境变量

#### 查看环境变量信息：go env

![image-20200610222440467](C:\Users\RHW\AppData\Roaming\Typora\typora-user-images\image-20200610222440467.png)

# 下载并安装 VS Code

##### 安装 go 微软官方插件

##### 由于资源或者网络等限制，通常直接通过 vs code下载会失败

##### 在此需要先设置 `GOPROXY`， 打开终端执行以下命令

`go env -w GOPROXY=https://goproxy.cn,direct`

![image-20200611223359784](C:\Users\RHW\AppData\Roaming\Typora\typora-user-images\image-20200611223359784.png)

##### 此时下载成功！

# 编译

##### 使用 `go build` 命令

1. ###### 在项目目录下执行 go build，此时会在项目下生成对应的可执行文件（推荐）

2. ###### 在其他路径下执行 go build，需要在后面加上项目的路径（项目路径从 GOPATH/src 后开始写起），此时会在开始执行这个命令的路径下生成可执行文件

3. ###### `go build -o hello.exe` 可以通过 -o的方法来制定输出可执行文件的名称

### go 的其他命令

##### go run

像执行脚本文件一样执行 Go 代码 （go run main.go）



##### go install

`go install` 分为两步

1. 先编译得到一个可执行文件
2. 将可执行文件拷贝到 `GOPATH/bin`

---

### 跨平台编译

###### 默认我们`go build`的可执行文件都是当前操作系统可执行的文件，如果我想在windows下编译一个linux下可执行文件，那需要怎么做呢？

###### 只需要指定目标操作系统的平台和处理器架构即可

```bash
1.SET CGO_ENABLED=0  // 禁用CGO
2.SET GOOS=linux  // 目标平台是linux
3.SET GOARCH=amd64  // 目标处理器架构是amd64
```

*使用了cgo的代码是不支持跨平台编译的*

然后再执行`go build`命令，得到的就是能够在Linux平台运行的可执行文件了。

Mac 下编译 Linux 和 Windows平台 64位 可执行程序：

```bash
1.CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build
2.CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build
```

Linux 下编译 Mac 和 Windows 平台64位可执行程序：

```bash
1.CGO_ENABLED=0 GOOS=darwin GOARCH=amd64 go build
2.CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build
```

Windows下编译Mac平台64位可执行程序：

```bash
1.SET CGO_ENABLED=0
2.SET GOOS=darwin
3.SET GOARCH=amd64
4.go build
```



# Go语言文件的基本结构

```ba
//	导入语句
import "fmt"

//	函数外只能放置标识符（变量\常量\函数\类型）的声明
//	fmt.Println("Hello") // 非法

//	程序的入口函数
func main() {
	fmt.Println("Hello world")
}
```

# 变量和常量

[学习播客](https://liwenzhou.com/posts/Go/01_var_and_const/)

#### 注意事项

* ###### 变量名推荐使用小驼峰命名法

* ###### Go语言中的变量必须先声明再使用

* ###### 非全局变量声明且赋值后必须使用

###### 

# 数据类型

[学习播客](https://liwenzhou.com/posts/Go/02_datatype/)

#### fmt占位符

```go
//	fmt占位符
func main() {
	var n = 100
	//	查看类型
	fmt.Printf("%T\n", n)
	//	查看变量的值
	fmt.Printf("%v\n", n)
	//	查看十进制
	fmt.Printf("%d\n", n)
	//	查看二进制
	fmt.Printf("%b\n", n)
	//	查看八进制
	fmt.Printf("%o\n", n)
	//	查看十六进制
	fmt.Printf("%x\n", n)
	
	var s = "hello 沙河"
	//	查看字符串类型
	fmt.Printf("%s\n", s)
	//	查看变量的值
	fmt.Printf("%v\n", s)	//	万能
	//	给具体类型加上描述符
	fmt.Printf("%#v\n", s)	//	输出 =》 "hello 沙河"
	
}
```



## 字符串

###### Go语言中字符串是用双引号引用的

###### Go语言中单引号包裹的是字符

```go
//	字符串
s := "hello 沙河"	//	string类型
//	单独的字母、汉字、符号表示一个字符
c1 := 'h'	//	int32类型
c2 := '1'
c3 := '沙'
//	字节：1字节 = 8Bit（8个二进制位）
//	1个字符 'A' = 1个字节
//	1个utf8编码的汉字 '沙' = 一般占3个字节
```



# if 判断和 for 循环

[学习博客](https://liwenzhou.com/posts/Go/04_basic/)

### if 判断

```go
// if条件判断
func main() {
	// age := 19

	// if age > 18 { // 如果 age > 18 就执行这个{}中的代码
	// 	fmt.Println("澳门首家线上赌场开业啦！")
	// } else { // 否则就执行这个{}中的代码
	// 	fmt.Println("改写暑假作业啦！")
	// }

	// 多个判断条件
	// if age > 35 {
	// 	fmt.Println("人到中年")
	// } else if age > 18 {
	// 	fmt.Println("青年")
	// } else {
	// 	fmt.Println("好好学习！")
	// }

	// 作用域
	// age变量此时只在if条件判断语句中生效
	if age := 19; age > 18 { // 如果 age > 18 就执行这个{}中的代码
		fmt.Println("澳门首家线上赌场开业啦！")
	} else { // 否则就执行这个{}中的代码
		fmt.Println("改写暑假作业啦！")
	}

	// fmt.Println(age) // 在这里是找不到age
}
```

### for 循环

```go
func main() {
	// 基本格式
	// for i := 0; i < 10; i++ {
	// 	fmt.Println(i)
	// }

	// 变种1
	// var i = 5
	// for ; i < 10; i++ {
	// 	fmt.Println(i)
	// }
	// 变种2
	// var i = 5
	// for i < 10 {
	// 	fmt.Println(i)
	// 	i++
	// }

	// 无限循环
	// for {
	// 	fmt.Println("123")
	// }

	// for range循环
	s := "Hello沙河"
	for i, v := range s {
		fmt.Printf("%d %c\n", i, v)
	}
}
```

### 作业

---

1. 常量声明及练习题回去自己写一下，特别是iota定义数量级时（1024）
2. 编写代码分别定义一个整型、浮点型、布尔型、字符串型变量，使用`fmt.Printf()`搭配`%T`分别打印出上述变量的值和类型。
3. 编写代码统计出字符串`"hello沙河小王子"`中汉字的数量。(自己查资料)
4. 打印9*9乘法表

# switch

```go
func switchDemo1() {
	finger := 3
	switch finger {
	case 1:
		fmt.Println("大拇指")
	case 2:
		fmt.Println("食指")
	case 3:
		fmt.Println("中指")
	case 4:
		fmt.Println("无名指")
	case 5:
		fmt.Println("小拇指")
	default:
		fmt.Println("无效的输入！")
	}
}
```

### 注意：不同于java和js，go中的switch不需要在每个case下加break

###### 一个分支可以有多个值，多个case值中间使用英文逗号分隔。

```go
func testSwitch3() {
	switch n := 7; n {
	case 1, 3, 5, 7, 9:
		fmt.Println("奇数")
	case 2, 4, 6, 8:
		fmt.Println("偶数")
	default:
		fmt.Println(n)
	}
}
```



# 运算符

[学习播客](https://liwenzhou.com/posts/Go/03_operators/)

##### Go 语言内置的运算符有：

1. ###### 算数运算符

2. ###### 关系运算符

3. ###### 逻辑运算符

4. ###### 位运算符

5. ###### 赋值运算符

### 难点：位运算符

```go
//	位运算：针对的是二进制
//	5的二进制表示的是：101
//	2的二进制表示的是：10

//	& :按位与（两位均为1才为1）
fmt.Println(5 & 2)	//	000 => 0
//	|：按位或（两位有1个为1就为1）
fmt.Println(5 | 2)	//	111 => 7
//	^：按位异或（两位不一样则为1）
fmt.Println(5 ^ 2)	// 111 => 7
//	<<：将二进制位左移指定位数
fmt.Println(5 << 1) // 1010 => 10
fmt.Println(1 << 10) // 10000000000 => 1024
//	>>：将二进制位右移指定的位数
fmt.Println(5 >> 2) //	1 => 1
```



# 复合数据类型

## 数组(Array)

[学习博客](https://liwenzhou.com/posts/Go/05_array/)

#### 数组的定义

```go
var 数组变量名 [元素数量]T
var a [3]int
```

1. ###### 存放元素的容器

2. ###### 必须制定存放的元素的类型和容量（长度）

3. ###### 数组的长度是数组类型的一部分

#### 数组的初始化

###### 如果不初始化：默认元素都是零值（布尔值：false，整形和浮点型都是0，字符串： ""）

##### 方法一

```go
a1 = [3]bool{true, true, true}
```

##### 方法二

```go
//	根据初始值自动推断数组的长度是多少
a10 := [...]int{1, 2, 3, 4, 5, 6, 7}
```

##### 方法三（1）

```go
//	自动补齐数组
a3 := [5]int{0, 1}
fmt.Println(a3)	//	a3: [0 1 0 0 0]
```

##### 方法三（2）

```go
//	根据索引来初始化
a4 := [5]int{0: 1, 4: 2}
fmt.Println(a4)	//	a4: [1 0 0 0 2]
```

### 数组的遍历

```go
citys := [...]string{"北京", "上海", "深圳"}
```



#### 1. 根据索引遍历

```go
for i := 0; i < len(citys); i++ {
    fmt.Println(citys[i])
}
```

#### 2. for range遍历

```go
for i, v := range citys {
    fmt.Println(i, v)
}
//	如果不想打印出索引i，可以使用 _ 替代i
for _, v := range citys {
    fmt.Println(i, v)
}
```

### 多维数组（数组中又嵌套数组）

##### 多维数组的定义

```go
a := [3][2]string{
    {"北京", "上海"},
    {"广州", "深圳"},
    {"成都", "重庆"},	//	逗号必须加上，否则报错
}
fmt.Println(a) //[[北京 上海] [广州 深圳] [成都 重庆]]
fmt.Println(a[2][1]) //支持索引取值:重庆
```

##### 多维数组遍历

```go
a := [3][2]string{
    {"北京", "上海"},
    {"广州", "深圳"},
    {"成都", "重庆"},
}
for _, v1 := range a {
    for _, v2 := range v1 {
        fmt.Printf("%s\t", v2)
    }
    fmt.Println()
}

//	输出
    北京	上海	
    广州	深圳	
    成都	重庆	
```



### 数组是值类型

```go
//	数组是值类型
b1 := [3]int{1, 2, 3} //	b1: [1 2 3]
b2 := b1              //	b2: [1 2 3] 类似于Ctrl+C  Ctrl+V 不会改变原来的值
b2[0] = 100           //	b2: [100 2 3]
fmt.Println(b1, b2)   //	b1: [1 2 3], b2: [100 2 3]
```

#### 注意：

1. ###### 数组支持 “==“、”!=” 操作符，因为内存总是被初始化过的。

2. ###### `[n]*T`表示指针数组，`*[n]T`表示数组指针 。

## 切片（slice）



切片指向了一个底层的数组。

切片的长度就是它元素的个数。

切片的容量是底层数组从切片的第一个元素到最后一个元素的数量。

### 切片的定义

```go
// 切片的定义
var s1 []int    // 定义一个存放int类型元素的切片
var s2 []string // 定义一个存放string类型元素的切片
fmt.Println(s1, s2)
fmt.Println(s1 == nil) // true
fmt.Println(s2 == nil) // true
```

### 切片的初始化

```go
// 初始化
s1 = []int{1, 2, 3}
s2 = []string{"沙河", "张江", "平山村"}
fmt.Println(s1, s2)
fmt.Println(s1 == nil) // false
fmt.Println(s2 == nil) // false
```

### 切片的长度和容量

```go
// 长度和容量
fmt.Printf("len(s1):%d cap(s1):%d\n", len(s1), cap(s1))
fmt.Printf("len(s2):%d cap(s2):%d\n", len(s2), cap(s2)
```



### make

make()函数用于创建指定长度和容量的切片。

```go
s1 := make([]int, 5, 10)
fmt.Printf("s1=%v len(s1)=%d cap(s1)=%d\n", s1, len(s1), cap(s1))

s2 := make([]int, 0, 10)
fmt.Printf("s1=%v len(s1)=%d cap(s1)=%d\n", s2, len(s2), cap(s2))
```

### 切片的本质

切片就是一个框，框住了一块连续的内存。

切片属于引用类型，真正的数据都是保存在底层数组里的。



判断一个切片是否是空的，要是用`len(s) == 0`来判断

### append

```go
// 调用append函数必须用原来的切片变量接收返回值
// append追加元素，原来的底层数组放不下的时候，Go底层就会把底层数组换一个
// 必须用变量接收append的返回值
s1 = append(s1, "广州")
fmt.Printf("s1=%v len(s1)=%d cap(s1)=%d\n", s1, len(s1), cap(s1))
s1 = append(s1, "杭州", "成都")
fmt.Printf("s1=%v len(s1)=%d cap(s1)=%d\n", s1, len(s1), cap(s1))
ss := []string{"武汉", "西安", "苏州"}
s1 = append(s1, ss...) // ...表示拆开
fmt.Printf("s1=%v len(s1)=%d cap(s1)=%d\n", s1, len(s1), cap(s1))
```

### copy

```go
a1 := []int{1, 3, 5}
a2 := a1 // 赋值
var a3 = make([]int, 3, 3)
copy(a3, a1) // copy
fmt.Println(a1, a2, a3)
a1[0] = 100
fmt.Println(a1, a2, a3)
```

## 指针

###### Go语言中不存在指针操作，只需要记住两个符号：

1. ###### `&`:取地址

2. ###### `*`:根据地址取值

## make和new的区别

1. ###### make和new都是用来申请内存的

2. ###### new很少用，一般用来给基本数据类型申请内存，`string`、`int`,返回的是对应类型的指针(\*string、\*int)。

3. ###### make是用来给`slice`、`map`、`chan`申请内存的，make函数返回的的是对应的这三个类型本身

## map

[学习博客](https://www.liwenzhou.com/posts/Go/08_map/)

map存储的是键值对的数据。

也是需要申请内存的。

###### map也是引用类型，必须初始化之后才能使用。

###### `go doc builtin.delete`    查看文档命令

###### [Golang标准库文档](https://studygolang.com/pkgdoc)



## 函数

### 函数的定义

#### 基本格式

```go
func f1() {
	fmt.Println("Hello 沙河！")
}
```

#### 参数的格式

有参数的函数

```go
func f2(name string) {
	fmt.Println("Hello", name)
}

```

参数类型简写

```go
// 参数类型简写
func f4(x, y int) int {
	return x + y
}
```

可变参数

```go
// 可变参数
func f5(title string, y ...int) int {
	fmt.Println(y) // y是一个int类型的切片
	return 1
}

```

#### 返回值的格式

有返回值

```go
// 带参数和返回值的函数
func f3(x int, y int) int {
	sum := x + y
	return sum
}
```

多返回值

```go
// Go语言中支持多个返回值
func f7(x, y int) (sum int, sub int) {
	sum = x + y
	sub = x - y
	return
}
```

命名返回值

```go
// 命名返回值
func f6(x, y int) (sum int) {
	sum = x + y // 如果使用命名的返回值，那么在函数中可以直接使用返回值变量
	return      // 如果使用命名的返回值,return后面可以省略返回值变量
}
```



### 变量作用域

1. 全局作用域
2. 函数作用域
   1. 先在函数内部找变量，找不到往外层找
   2. 函数内部的变量，外部是访问不到的
3. 代码块作用域

```go
var x = 100 // 定义一个全局变量

// 定义一个函数
func f1() {
	// x := 10
	name := "理想"
	// 函数中查找变量的顺序
	// 1. 先在函数内部查找
	// 2. 找不到就往函数的外面查找,一直找到全局
	fmt.Println(x, name)
}

func main() {
	f1()
	// fmt.Println(name) // 函数内部定义的变脸只能在该函数内部使用

	// 语句块作用域
	if i := 10; i < 18 {
		fmt.Println("乖乖上学")
	}
	// fmt.Println(i) // 不存在i
	for j := 0; j < 5; j++ {
		fmt.Println(j)
	}
	// fmt.Println(j) // 不存在j
}
```

### 高阶函数

函数也是一种类型，它可以作为参数，也可以作为返回值。

```go
// 函数也可以作为参数的类型
func f3(x func() int) {
	ret := x()
	fmt.Println(ret)
}

func ff(a, b int) int {
	return a + b
}

// 函数还可以作为返回值
func f5(x func() int) func(int, int) int {
	return ff
}
```



### 匿名函数

没有名字的函数。

多用在函数内部定义函数时使用。

```go
func main() {

	// 函数内部没有办法声明带名字的函数
	// 匿名函数
	f1 := func(x, y int) {
		fmt.Println(x + y)
	}
	f1(10, 20)

	// 如果只是调用一次的函数，还可以简写成立即执行函数
	func(x, y int) {
		fmt.Println(x + y)
		fmt.Println("Hello world!")
	}(100, 200)
}
```

### 闭包

![1563005182920](F:/golang%E6%95%99%E7%A8%8B/day03/%E8%A7%86%E9%A2%91/day03%E8%AF%BE%E4%B8%8A%E4%BB%A3%E7%A0%81%E5%92%8C%E7%AC%94%E8%AE%B0/day03/assets/1563005182920.png)



### defer

defer延迟调用，会把defer后面的语句延迟调用

把当时的状态都保存

defer多用于释放资源

多个defer存在时，按照先进后出的方式去执行。

```go
func calc(index string, a, b int) int {
	ret := a + b
	fmt.Println(index, a, b, ret)
	return ret
}

func main() {
	a := 1
	b := 2
	defer calc("1", a, calc("10", a, b))
	a = 0
	defer calc("2", a, calc("20", a, b))
	b = 1
}

// 1. a:=1
// 2. b:=2
// 3. defer calc("1", 1, calc("10", 1, 2))
// 4. calc("10", 1, 2) // "10" 1 2 3
// 5. defer calc("1", 1, 3)
// 6. a = 0
// 7. defer calc("2", 0, calc("20", 0, 2))
// 8. calc("20", 0, 2) // "20" 0 2 2
// 9. defer calc("2", 0, 2)
// 10. b = 1
// calc("2", 0, 2) // "2" 0 2 2
// calc("1", 1, 3) // "1" 1 3 4

// 最终的答案：
// "10" 1 2 3
// "20" 0 2 2
//  "2" 0 2 2
// "1" 0 3 3
```



### 内置函数

![1563014612689](F:/golang%E6%95%99%E7%A8%8B/day03/%E8%A7%86%E9%A2%91/day03%E8%AF%BE%E4%B8%8A%E4%BB%A3%E7%A0%81%E5%92%8C%E7%AC%94%E8%AE%B0/day03/assets/1563014612689.png)

### panic和recover

```go
func funcA() {
	fmt.Println("a")
}

func funcB() {
	// 刚刚打开数据库连接
	defer func() {
		err := recover()
		fmt.Println(err)
		fmt.Println("释放数据库连接...")
	}()
	panic("出现了严重的错误！！！") // 程序崩溃退出
	fmt.Println("b")
}

func funcC() {
	fmt.Println("c")
}
func main() {
	funcA()
	funcB()
	funcC()
}
```

### 今天的难点

1. 函数的定义
2. 高阶函数
3. 函数类型
4. 闭包
5. defer
6. panic/revocer

# 本周作业

1. 分金币作业

   ```go
   /*
   你有50枚金币，需要分配给以下几个人：Matthew,Sarah,Augustus,Heidi,Emilie,Peter,Giana,Adriano,Aaron,Elizabeth。
   分配规则如下：
   a. 名字中每包含1个'e'或'E'分1枚金币
   b. 名字中每包含1个'i'或'I'分2枚金币
   c. 名字中每包含1个'o'或'O'分3枚金币
   d: 名字中每包含1个'u'或'U'分4枚金币
   
   写一个程序，计算每个用户分到多少金币，以及最后剩余多少金币？
   程序结构如下，请实现 ‘dispatchCoin’ 函数
   */
   var (
   	coins = 5000
   	users = []string{
   		"Matthew", "Sarah", "Augustus", "Heidi", "Emilie", "Peter", "Giana", "Adriano", "Aaron", "Elizabeth",
   	}
   	distribution = make(map[string]int, len(users))
   )
   
   func main() {
   	left := dispatchCoin()
   	fmt.Println("剩下：", left)
   }
   
   func dispatchCoin() (left int) {
   	// 1. 依次拿到每个人的名字
   	// 2. 拿到一个人名根据分金币的规则去分金币,
   	// 2.1 每个人分的金币数应该保存到 distribution 中
   	// 2.2 还要记录下剩余的金币数
   	// 3. 整个第2步执行完就能得到最终每个人分的金币数和剩余金币数
   	return
   }
   ```

   

2. 预习结构体[https://www.liwenzhou.com/posts/Go/10_struct/](



# GoS5 day04 

# 内容回顾

函数

函数的定义

```go
func 函数名(参数1, 参数2...)返回值{
    函数体
}
```



函数进阶

​	高阶函数:函数可以作为参数也可以作为返回值

​	闭包 :函数和其外部变量的引用

​	defer:延迟调用,多用于处理资源释放

​	内置函数:

​		`panic`和`recover`:

作业

​	分金币作业

补充递归函数:

1. 阶乘的例子
2. 台阶面试题

# 今日内容

结构体(struct)

### 结构体定义

```go
type 结构体名 struct{
    字段1 字段1的类型
    字段2 字段2的类型
    ...
} 
```

### 结构体初始化

#### 先声明再赋值

```go
var p person // 声明一个person类型的变量p
p.name = "元帅"
p.age = 18
fmt.Println(p)
```

#### 声明同时初始化 

键值对初始化

```go
// 键值对初始化
var p2 = person{
	name: "冠华",
	age:  15,
}
fmt.Println(p2)
```

值列表初始化

```go
// 值列表初始化
var p3 = person{
	"理想",
	100,
}
fmt.Println(p3)
```

#### 注意事项:

1. 两者不能混用
2. 没有赋值的字段会使用对应类型的零值.

### 结构体指针

结构体是值类型,赋值的时候都是拷贝.

当结构体字段较多的时候,为了减少内存消耗可以传递结构体指针.

### 构造函数

返回一个结构体变量的函数,为了实例化结构体的时候更省事儿.

```go
func newPerson(name string, age int)person{
    return person{
        name: name,
        age: age,
    }
}
```

### 方法

方法是作用于特定类型的函数.

方法的定义:(万变不离其宗)

```go
func (接收者变量 接收者类型)方法名(参数)返回值{
    // 方法体
}
```

#### 接收者

接收者通常使用类型首字母的小写,不建议使用诸如`this`和`self`这样的.

### 值接收者和指针接收者的区别

使用值接收者的方法不能修改结构体变量

使用指针接收者的方法可以修改结构体的变量,课上过年长一岁的例子.

![1563616941046](F:/golang%E6%95%99%E7%A8%8B/day04/%E8%A7%86%E9%A2%91/day04%E8%AF%BE%E4%B8%8A%E4%BB%A3%E7%A0%81%E5%92%8C%E7%AC%94%E8%AE%B0/day04/assets/1563616941046.png)

我们应该尽量使用指针接收者.

### 标识符

// 标识符:变量名 函数名 类型名 方法名

// Go语言中如果标识符首字母是大写的,就表示对外部包可见(暴露的,公有的).

### 匿名字段

没有名字的字段.

### 嵌套结构体

```go
type address struct {
	province string
	city     string
}

type company struct {
	name string
	addr address // 嵌套
}

```

### 匿名嵌套结构体

```go
type address struct {
	province string
	city     string
}

type company struct {
	name string
	address // 嵌套匿名结构体
}

```



### 匿名嵌套结构体的字段冲突

先在自己结构体找这个字段,找不到就去匿名嵌套的结构体中查找该字段

```go
type address struct {
	province string
	city     string
}

type workPlace struct {
	province string
	city     string
}

type person struct {
	name    string
	age     int
	address   // 匿名嵌套结构体
	workPlace // 匿名嵌套结构体
}

```

## 结构体与JSON

JSON:是一种跨语言的数据格式.多用于在不同语言间传递数据

```go
// 1.序列化:   把Go语言中的结构体变量 --> json格式的字符串
// 2.反序列化: json格式的字符串   --> Go语言中能够识别的结构体变量

type person struct {
	Name string `json:"name" db:"name" ini:"name"`
	Age  int    `json:"age"`
}

func main() {
	p1 := person{
		Name: "周林",
		Age:  9000,
	}
	// 序列化
	b, err := json.Marshal(p1)
	if err != nil {
		fmt.Printf("marshal failed, err:%v", err)
		return
	}
	fmt.Printf("%v\n", string(b))
	// 反序列化
	str := `{"name":"理想","age":18}`
	var p2 person
	json.Unmarshal([]byte(str), &p2) // 传指针是为了能在json.Unmarshal内部修改p2的值
	fmt.Printf("%#v\n", p2)
}

```

# 作业

1. 把课上写的代码都自己敲一遍
2. 把课上写的函数版学生信息管理系统自己写一遍
3. 把函数版学员信息管理系统改写成方法版.(提示:谁的方法)





# day05课上笔记

# 内容回顾

### 自定义类型和类型别名

```go
type MyInt int // 自定义类型
type newInt = int // 类型别名
```

类型别名只在代码编写 过程中有效,编译完之后就不存在,内置的`byte`和`rune`都属于类型别名.

## 结构体

基本的数据类型:表示现实中的物件有局限性.

编程是代码解决现实生活中的问题.

```go
var name = "保德路"
```

结构体是一种数据类型,一种我们自己造的可以保存多个维度数据的类型.

```go
type person struct {
    name string
    age int
   	id int64
    addr string
}
```

匿名结构体

多用于临时场景.

```go
var a = struct{
    x int
    y int
}
```

结构体的初始化

![1564193680214](F:/golang%E6%95%99%E7%A8%8B/day05/%E8%A7%86%E9%A2%91/day05%E8%AF%BE%E4%B8%8A%E4%BB%A3%E7%A0%81%E5%92%8C%E7%AC%94%E8%AE%B0/day05/assets/1564193680214.png)

构造函数

![1564193780693](F:/golang%E6%95%99%E7%A8%8B/day05/%E8%A7%86%E9%A2%91/day05%E8%AF%BE%E4%B8%8A%E4%BB%A3%E7%A0%81%E5%92%8C%E7%AC%94%E8%AE%B0/day05/assets/1564193780693.png)

![1564193857316](F:/golang%E6%95%99%E7%A8%8B/day05/%E8%A7%86%E9%A2%91/day05%E8%AF%BE%E4%B8%8A%E4%BB%A3%E7%A0%81%E5%92%8C%E7%AC%94%E8%AE%B0/day05/assets/1564193857316.png)



### 方法和接收者

方法是有接收者的函数,接收者指的是哪个类型的变量可以调用这个函数.

![1564194291078](F:/golang%E6%95%99%E7%A8%8B/day05/%E8%A7%86%E9%A2%91/day05%E8%AF%BE%E4%B8%8A%E4%BB%A3%E7%A0%81%E5%92%8C%E7%AC%94%E8%AE%B0/day05/assets/1564194291078.png)



结构体是值类型,

![1564194808166](F:/golang%E6%95%99%E7%A8%8B/day05/%E8%A7%86%E9%A2%91/day05%E8%AF%BE%E4%B8%8A%E4%BB%A3%E7%A0%81%E5%92%8C%E7%AC%94%E8%AE%B0/day05/assets/1564194808166.png)



结构体的嵌套

![1564194949747](F:/golang%E6%95%99%E7%A8%8B/day05/%E8%A7%86%E9%A2%91/day05%E8%AF%BE%E4%B8%8A%E4%BB%A3%E7%A0%81%E5%92%8C%E7%AC%94%E8%AE%B0/day05/assets/1564194949747.png)



结构体的匿名字段

![1564194990771](F:/golang%E6%95%99%E7%A8%8B/day05/%E8%A7%86%E9%A2%91/day05%E8%AF%BE%E4%B8%8A%E4%BB%A3%E7%A0%81%E5%92%8C%E7%AC%94%E8%AE%B0/day05/assets/1564194990771.png)

### JSON序列化与反序列化

经常出现问题:

1. 架构体内部的字段首字母要大写!!!不大写别人是访问不到
2. 反序列化时要传递指针!

![1564195273460](F:/golang%E6%95%99%E7%A8%8B/day05/%E8%A7%86%E9%A2%91/day05%E8%AF%BE%E4%B8%8A%E4%BB%A3%E7%A0%81%E5%92%8C%E7%AC%94%E8%AE%B0/day05/assets/1564195273460.png)

![1564195837883](F:/golang%E6%95%99%E7%A8%8B/day05/%E8%A7%86%E9%A2%91/day05%E8%AF%BE%E4%B8%8A%E4%BB%A3%E7%A0%81%E5%92%8C%E7%AC%94%E8%AE%B0/day05/assets/1564195837883.png)

# 今日内容

## 接口(interface) 

[博客:https://www.liwenzhou.com/posts/Go/12_interface/](https://www.liwenzhou.com/posts/Go/12_interface/)

接口是一种类型,是一种特殊的类型,它规定了变量有哪些方法.

在编程中会遇到以下场景:

我不关心一个变量是什么类型,我只关心能调用它的什么方法.

### 接口的定义

```go
type 接口名 interface {
    方法名1(参数1,参数2...)(返回值1, 返回值2...)
    方法名2(参数1,参数2...)(返回值1, 返回值2...)
    ...
}
```

用来给变量\参数\返回值等设置类型.

### 接口的实现

一个变量如果实现了接口中规定的所有的方法,那么这个变量就实现了这个接口,可以称为这个接口类型的变量.

![1564211085692](F:/golang%E6%95%99%E7%A8%8B/day05/%E8%A7%86%E9%A2%91/day05%E8%AF%BE%E4%B8%8A%E4%BB%A3%E7%A0%81%E5%92%8C%E7%AC%94%E8%AE%B0/day05/assets/1564211085692.png)



![1564211890251](F:/golang%E6%95%99%E7%A8%8B/day05/%E8%A7%86%E9%A2%91/day05%E8%AF%BE%E4%B8%8A%E4%BB%A3%E7%A0%81%E5%92%8C%E7%AC%94%E8%AE%B0/day05/assets/1564211890251.png)

### 使用值接收者实现接口与使用指针接收者实现接口的区别?

使用值接收者实现接口,结构体类型和结构体指针类型的变量都能存.

指针接收者实现接口只能存结构体指针类型的变量.

### 接口和类型的关系

多个类型可以实现同一个接口.

一个类型可以实现多个接口.

![1564213783276](F:/golang%E6%95%99%E7%A8%8B/day05/%E8%A7%86%E9%A2%91/day05%E8%AF%BE%E4%B8%8A%E4%BB%A3%E7%A0%81%E5%92%8C%E7%AC%94%E8%AE%B0/day05/assets/1564213783276.png)

### 接口可以嵌套

![1564213756671](F:/golang%E6%95%99%E7%A8%8B/day05/%E8%A7%86%E9%A2%91/day05%E8%AF%BE%E4%B8%8A%E4%BB%A3%E7%A0%81%E5%92%8C%E7%AC%94%E8%AE%B0/day05/assets/1564213756671.png)



### 空接口

没有必要起名字,通常定义成下面的格式:

```go
interface{} // 空接口
```

所有的类型都实现了空接口.也就是任意类型的变量都能保存到空接口中.

![1564216843178](F:/golang%E6%95%99%E7%A8%8B/day05/%E8%A7%86%E9%A2%91/day05%E8%AF%BE%E4%B8%8A%E4%BB%A3%E7%A0%81%E5%92%8C%E7%AC%94%E8%AE%B0/day05/assets/1564216843178.png)



## 包(package)

[博客:https://www.liwenzhou.com/posts/Go/11_package/](https://www.liwenzhou.com/posts/Go/11_package/)

- 包的路径从`GOPATH/src`后面的路径开始写起,路径分隔符用`/`
- 想被别的包调用的标识符都要首字母大写!
- 单行导入和多行导入
- 导入包的时候可以指定别名
- 导入包不想使用包内部的标识符,需要使用匿名导入
- 每个包导入的时候会自动执行一个名为`init()`的函数,它没有参数也没有返回值也不能手动调用
- 多个包中都定义了`init()`函数,则它们的执行顺序见下图:

![1564219349069](F:/golang%E6%95%99%E7%A8%8B/day05/%E8%A7%86%E9%A2%91/day05%E8%AF%BE%E4%B8%8A%E4%BB%A3%E7%A0%81%E5%92%8C%E7%AC%94%E8%AE%B0/day05/assets/1564219349069.png)

## 文件操作

[博客:https://www.liwenzhou.com/posts/Go/go_file/](https://www.liwenzhou.com/posts/Go/go_file/)

```go
package main

import (
        "fmt"
        "os"
)

// 打开文件

func main() {
        fileObj, err := os.Open("./main.go")
        if err !
读了128个字节
= nil {
                fmt.Printf("open file failed, err:%v", err)
                return
        }
        // 记得关闭文件
        defer fileObj.Close()
        // 读文
读了128个字节
件
        // var tmp = make([]byte, 128) // 指定读的长度
        var tmp [128]byte
        for {
                n, err := fileObj.Read(tmp[:])
                if e
读了128个字节
rr != nil {
                        fmt.Printf("read from file failed, err:%v", err)
                        return
                }
                fmt.Printf("读了%d个字节\n", n)
                fmt.
读了66个字节
Println(string(tmp[:n]))
                if n == 0 {
                        return
                }
        }

}
```

# 作业

1. 把课上读文件的3种方式写一遍
2. 把课上写文件的3种方式和copyFIle那个函数写一遍
3. 日志库

自己写一个日志库.

接口: 用处?日志可以输出到终端,也可以输出到文件,输出到kafka

需求:

1. 可以往不同的输出位置记录日志
2. 日志分为五种级别






























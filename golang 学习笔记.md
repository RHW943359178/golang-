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

###### map也是引用类型，必须初始化之后才能使用。

###### `go doc builtin.delete`    查看文档命令

###### [Golang标准库文档](https://studygolang.com/pkgdoc)
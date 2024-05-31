---
description: 良友
---

# ⭐ Go语言入门指南

### 什么是Go语言？



Go语言（简称Go或Golang）是由谷歌开发的一种开源编程语言，设计目的是提高编程效率，特别适用于开发高性能和高并发的服务器端应用。Go语言具有简单易学、高效和并发支持等特点。

### 安装Go语言



#### 步骤1：下载并安装



1. 访问[Go语言官网](https://github.com/AndsGo/notes/blob/master/blog)下载最新版本的安装包。
2. 根据操作系统选择对应的安装包并进行安装。

#### 步骤2：配置环境变量



安装完成后，需要配置环境变量以便在命令行中使用`go`命令。

* **Windows**：
  1. 右键“此电脑”，选择“属性”。
  2. 点击“高级系统设置”，然后点击“环境变量”。
  3. 在“系统变量”中找到`Path`，编辑并添加Go的安装路径（例如：`C:\Go\bin`）。
* **macOS和Linux**：
  1. 打开终端。
  2.  编辑

      ```
      ~/.bash_profile
      ```

      或

      ```
      ~/.zshrc
      ```

      文件，添加以下行：

      ```
      export PATH=$PATH:/usr/local/go/bin
      ```
  3. 保存文件并运行`source ~/.bash_profile`或`source ~/.zshrc`使更改生效。

#### 步骤3：验证安装



打开命令行工具，输入`go version`，如果显示Go的版本信息，则说明安装成功。

```
$ go version
go version go1.17.1 linux/amd64
```

### 编写第一个Go程序



#### 步骤1：创建工作目录



选择一个目录作为你的Go项目的工作空间。例如，可以在用户目录下创建一个`go-workspace`目录。

```
$ mkdir ~/go-workspace
$ cd ~/go-workspace
```

#### 步骤2：编写代码



在工作目录下创建一个名为`hello.go`的文件，并在其中编写如下代码：

```
package main

import "fmt"

func main() {
    fmt.Println("Hello, Go!")
}
```

#### 步骤3：运行程序



在命令行中进入文件所在目录，并运行以下命令编译并执行程序：

```
$ go run hello.go
```

如果一切顺利，你将看到如下输出：

```
Hello, Go!
```

### Go语言基础



#### 变量和常量



**变量**



使用`var`关键字声明变量：

```
//先声明后赋值
var name string
name = "Go"

//声明并同时赋值
var age int = 10

// 简短声明并赋值
language := "Go"
```

**常量**



使用`const`关键字声明常量：

```
const Pi = 3.14
const Language = "Go"
```

#### 数据类型



Go语言提供了多种基本数据类型：

* **整型**：int, int8, int16, int32, int64
* **无符号整型**：uint, uint8, uint16, uint32, uint64
* **浮点型**：float32, float64, complex64, complex128
* **布尔型**：bool
* **字符串**：string

**整型数据类型范围**

| 类型名称    | 大小      | 描述                                                                                                        |
| ------- | ------- | --------------------------------------------------------------------------------------------------------- |
| int     | 8 字节    | int的大小是和操作系统位数相关的，如果是32位操作系统，int类型的大小是4字节；如果是64位操作系统，int类型的大小就是8个字节                                       |
| int8    | 1 字节    | 无符号整数的所有bit位都用于表示非负数，值域是0到$2^n-1$。例如，int8类型整数的值域是从-128到127，而uint8类型整数的值域是从0到255。                          |
| int16   | 2 字节    | 有符号int16类型整数值域是从 -32768 \~ 32767，而无符号uint16类型整数值域是从 0 \~ 65535                                            |
| int32   | 4 字节    | 有符号int32类型整数值域是从 -2147483648 \~ 2147483647，而无符号uint32类型整数值域是从 0 \~ 4294967295                             |
| int64   | 8 字节    | 有符号int64类型整数值域是从 -9223372036854775808 \~ 9223372036854775807，而无符号uint64类型整数值域是从 0 \~ 18446744073709551615 |
| uintptr | 长度4或8字节 | 存储指针的uint32 或 uint64整数                                                                                    |

#### 整型使用建议



* **int**：在不需要特定大小的情况下使用。由于其大小依赖于平台，在编写与平台无关的代码时，使用 `int` 会更灵活。
* **int8, int16, int32, int64**：在需要特定整数大小时使用，例如在网络协议、文件格式或其他需要精确控制数据大小的情况下。

**浮点型数据类型范围**

| 大小    | 类型名称       | 描述                                    |
| ----- | ---------- | ------------------------------------- |
| 4 字节  | float32    | 单精度类型，占据4个字节byte，32个二进制位bit           |
| 8 字节  | float64    | 双精度类型比单精度类型更能精确地表示一个小数，但是占用的内存空间也比较大。 |
| 8 字节  | complex64  | 包含两个float32类型表示复数                     |
| 16 字节 | complex128 | 包含两个float64类型表示复数                     |

#### 浮点型使用建议



* **float32**：在内存和性能要求较高、精度需求相对较低的情况下使用。
* **float64**：在需要高精度浮点运算的情况下使用，这是最常用的浮点类型，适用于大多数科学和工程计算。
* **complex64**：在需要表示复数且对内存有严格控制的情况下使用。
* **complex128**：在需要高精度复数运算的情况下使用。

#### 控制结构



**条件语句**



```
if age > 18 {
    fmt.Println("Adult")
} else {
    fmt.Println("Minor")
}
```

**循环语句**



```
for i := 0; i < 5; i++ {
    fmt.Println(i)
}

// 通过range迭代切片或数组
numbers := []int{1, 2, 3, 4, 5}
for index, value := range numbers {
    fmt.Printf("Index: %d, Value: %d\n", index, value)
}
```

#### 函数



定义和调用函数：

```
func add(a int, b int) int {
    return a + b
}

result := add(3, 4)
fmt.Println(result)  // 输出: 7

// 函数可以返回多个值
func swap(x, y string) (string, string) {
    return y, x
}

a, b := swap("hello", "world")
fmt.Println(a, b)  // 输出: world hello
```

#### 数组和切片



**数组**



```
var arr [5]int
arr[0] = 1
arr[1] = 2
fmt.Println(arr)	//输出: [1 2 0 0 0]
```

**切片**



```
slice := []int{1, 2, 3, 4, 5}
fmt.Println(slice)	//输出[1 2 3 4 5]

newSlice := slice[1:3]
fmt.Println(newSlice)	//输出[2 3]
```

一个切片是一个数组片段的描述。它包含了指向数组的指针，片段的长度， 和容量（片段的最大长度）

#### 映射（Map）



```
m := make(map[string]int)
m["one"] = 1
m["two"] = 2
fmt.Println(m)	// 输出: map[one:1 two:2]

value, exists := m["one"]
if exists {
    fmt.Println(value)  // 输出: 1
}

// 删除键值对
delete(m, "two")
fmt.Println(m)	// map[one:1]
```

### 结构体和方法



#### 结构体



定义一个结构体类型并创建其实例：

```
type Person struct {
    Name string
    Age  int
}

p := Person{Name: "Alice", Age: 30}
fmt.Println(p)	// 输出: {Alice 30}
```

#### 方法



为结构体定义方法：

```
func (p Person) Greet() {
    fmt.Printf("Hello, my name is %s and I am %d years old.\n", p.Name, p.Age)
}

p.Greet()
```

#### 接口



接口是一组方法签名的集合：

```
type Greeter interface {
    Greet()
}

func greetAll(greeters []Greeter) {
    for _, greeter := range greeters {
        greeter.Greet()
    }
}

type Person struct {
    Name string
    Age  int
}

func (p Person) Greet() {
  // 输出:Hello, my name is Alice and I am 30 years old.
  fmt.Printf("Hello, my name is %s and I am %d years old.\n", p.Name, p.Age)	
}

p := Person{Name: "Alice", Age: 30}
greetAll([]Greeter{p})
```

### 并发编程



Go 允许使用 go 语句开启一个新的运行期线程， 即 goroutine **音标:\[gəu.ru'tin]**，以一个不同的、新创建的 goroutine 来执行一个函数。 同一个程序中的所有 goroutine 共享同一个地址空间。

Goroutine 可以理解为一种可以并发执行的函数或者任务。它们和线程类似，但更加轻量。在 Go 语言中，只需要用一个简单的关键词 `go` 就可以启动一个新的 goroutine

#### Goroutine



使用`go`关键字启动一个新的goroutine：

```
package main

import (
        "fmt"
        "time"
)

func say(s string) {
        for i := 0; i < 5; i++ {
                time.Sleep(100 * time.Millisecond)
                fmt.Println(s)
        }
}

func main() {
        go say("world")
        say("hello")
}
```

#### Channel



通过channel在goroutine之间传递数据：

```
ch := make(chan int)

go func() {
    ch <- 42
}()

value := <-ch
fmt.Println(value)  // 输出: 42
```

**带缓冲的Channel**



```
ch := make(chan int, 2)

ch <- 1
ch <- 2

fmt.Println(<-ch)  // 输出: 1
fmt.Println(<-ch)  // 输出: 2
```

**Select语句**



`select`语句用于处理多个channel操作：

```
ch1 := make(chan string)
ch2 := make(chan string)

go func() {
    ch1 <- "from ch1"
}()

go func() {
    ch2 <- "from ch2"
}()

select {
case msg1 := <-ch1:
    fmt.Println(msg1)
case msg2 := <-ch2:
    fmt.Println(msg2)
}
```

### 模块和包管理



Go语言的包管理系统使得代码组织和依赖管理变得简单。

#### 创建模块



创建一个新的Go模块：

```
$ mkdir mymodule
$ cd mymodule
$ go mod init mymodule
```

这将生成一个`go.mod`文件，记录模块的名称和依赖关系。

#### 导入包



创建一个新的Go文件`main.go`，并导入其他包：

```
package main

import (
    "fmt"
    "mymodule/mypackage"
)

func main() {
    fmt.Println("Hello, Go Modules!")
    mypackage.MyFunction()
}
```

在`mymodule`目录下创建一个子目录`mypackage`，并在其中创建一个新的Go文件`mypackage.go`：

```
package mypackage

import "fmt"

func MyFunction() {
    fmt.Println("Hello from mypackage!")
}
```

### 单元测试



Go语言内置了测试框架，通过编写测试文件来进行单元测试。

#### 编写测试



创建一个测试文件`main_test.go`：

```
package main

import "testing"

func TestAdd(t *testing.T) {
    result := add(3, 4)
    if result != 7 {
        t.Errorf("Expected 7, but got %d", result)
    }
}
```

#### 运行测试



使用`go test`命令运行测试：

```
$ go test
```

**遇到的问题: Goland 无法debug**

goland 调试的的时候提示如下错误

`WARNING: undefined behavior - version of Delve is too old for Go version 1.22.3 (maximum supported v`

其实个原因是因为正在使用的Delve调试器版本太旧，无法兼容当前的Go语言版本1.22.3。Delve是Go语言的一个调试工具，用于提供源码级别的调试功能。Go语言每隔一段时间会发布新版本，而相应的调试器Delve也可能会更新以提供新的特性或修复已知问题。

**解决步骤：**

_第一步：下载并安装，执行以下命令即可。_

`go install github.com/go-delve/delve/cmd/dlv@latest`

安装成功后，你会在自己的 GOPATH 目录的、bin目录下，看到dlv.exe的文件

然后最简单的方式 就是 用这个最新的dlv.exe文件 去替换自己goland 目录下的 旧的dlv.exe文件，

`{goland安装目录}\plugins\go\lib\dlv\windows\dlv.exe`

最后重启goland 就可以了

### 小结



本深入指南详细介绍了Go语言的基础知识和一些高级特性，包括变量、数据类型、控制结构、函数、结构体、接口、并发编程、模块和包管理以及单元测试。

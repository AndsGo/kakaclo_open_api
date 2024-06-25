# Go开发规范

### [基本规范](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E5%9F%BA%E6%9C%AC%E8%A7%84%E8%8C%83) <a href="#ji-ben-gui-fan" id="ji-ben-gui-fan"></a>

#### [限制单行长度](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E9%99%90%E5%88%B6%E5%8D%95%E8%A1%8C%E9%95%BF%E5%BA%A6) <a href="#xian-zhi-dan-hang-chang-du" id="xian-zhi-dan-hang-chang-du"></a>

Go 代码行长度限制为 80 个字符。这有助于在较小的窗口中查看多个文件，以及在较大的窗口中查看多个文件。

#### [相关的声明放在一起,不相关的声明不要放一起](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E7%9B%B8%E5%85%B3%E7%9A%84%E5%A3%B0%E6%98%8E%E6%94%BE%E5%9C%A8%E4%B8%80%E8%B5%B7-%E4%B8%8D%E7%9B%B8%E5%85%B3%E7%9A%84%E5%A3%B0%E6%98%8E%E4%B8%8D%E8%A6%81%E6%94%BE%E4%B8%80%E8%B5%B7) <a href="#xiang-guan-de-sheng-ming-fang-zai-yi-qi-bu-xiang-guan-de-sheng-ming-bu-yao-fang-yi-qi" id="xiang-guan-de-sheng-ming-fang-zai-yi-qi-bu-xiang-guan-de-sheng-ming-bu-yao-fang-yi-qi"></a>

如导入，常量，变量，类型，函数等。

| 不推荐                                                                                                                                                                 | 推荐                                                                                                                                                                                |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <pre><code>import "a"
import "b"
</code></pre>                                                                                                                      | <pre><code>import (
  "a"
  "b"
)
</code></pre>                                                                                                                                   |
| <pre><code>const a = 1
const b = 2

var a = 1
var b = 2

type Area float64
type Volume float64
</code></pre>                                                        | <pre><code>const (
  a = 1
  b = 2
)

var (
  a = 1
  b = 2
)

type (
  Area float64
  Volume float64
)
</code></pre>                                                             |
| <p>EnvVar 不属于 iota 相关</p><pre><code>type Operation int

const (
  Add Operation = iota + 1
  Subtract
  Multiply
  EnvVar = "MY_ENV"
)
</code></pre>                | <pre><code>type Operation int

const (
  Add Operation = iota + 1
  Subtract
  Multiply
)

const EnvVar = "MY_ENV"
</code></pre>                                                  |
| <pre><code>func f() string {
  red := color.New(0xff0000)
  green := color.New(0x00ff00)
  blue := color.New(0x0000ff)

  ...
}
</code></pre>                       | <p>函数内也可分组放在一起</p><pre><code>func f() string {
  var (
    red   = color.New(0xff0000)
    green = color.New(0x00ff00)
    blue  = color.New(0x0000ff)
  )

  ...
}
</code></pre> |
| <pre><code>func (c *client) request() {
  caller := c.name
  format := "json"
  timeout := 5*time.Second
  var err error // 单独使用 var 声明不规范
  // ...
}
</code></pre> | <pre><code>func (c *client) request() {
  var (
    caller  = c.name
    format  = "json"
    timeout = 5*time.Second
    err error
  )
  // ...
}
</code></pre>                  |

#### [单个变量声明规范](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E5%8D%95%E4%B8%AA%E5%8F%98%E9%87%8F%E5%A3%B0%E6%98%8E%E8%A7%84%E8%8C%83) <a href="#dan-ge-bian-liang-sheng-ming-gui-fan" id="dan-ge-bian-liang-sheng-ming-gui-fan"></a>

如果单个变量赋值，建议使用 `:=`， 但是切片建议使用 `var` 声明。

| 不推荐                                                                                                                                                             | 推荐                                                                                                                                                             |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <pre><code>var s = "foo"
</code></pre>                                                                                                                          | <pre><code>s := "foo"
</code></pre>                                                                                                                            |
| <pre><code>func f(list []int) {
  filtered := []int{}
  for _, v := range list {
    if v > 10 {
      filtered = append(filtered, v)
    }
  }
}
</code></pre> | <pre><code>func f(list []int) {
  var filtered []int
  for _, v := range list {
    if v > 10 {
      filtered = append(filtered, v)
    }
  }
}
</code></pre> |

#### [import 分组规范](https://goguide.ryansu.tech/guide/standard/1-golang.html#import-%E5%88%86%E7%BB%84%E8%A7%84%E8%8C%83) <a href="#import-fen-zu-gui-fan" id="import-fen-zu-gui-fan"></a>

`import` 导入的包应该进行分组，每组之间用空行分隔，每组按照字母顺序排序。

常用分组规则

分两组：

* 标准库
* 第三方库

分三组：

* 标准库
* 第三方库
* 本地库和私有库

| 不推荐                                                                                                      | 推荐                                                                                                        |
| -------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| <pre><code>import (
  "fmt"
  "os"
  "go.uber.org/atomic"
  "golang.org/x/sync/errgroup"
)
</code></pre> | <pre><code>import (
  "fmt"
  "os"

  "go.uber.org/atomic"
  "golang.org/x/sync/errgroup"
)
</code></pre> |

#### [导入别名](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E5%AF%BC%E5%85%A5%E5%88%AB%E5%90%8D) <a href="#dao-ru-bie-ming" id="dao-ru-bie-ming"></a>

如果导入的包名与导入路径中的最后一个单词不一致，应该使用别名。或者导入包名太长时可以使用导入别名。在通常情况下不推荐使用别名，除非包名冲突。

```
import (
  "net/http"

  client "example.com/client-go"
  trace "example.com/trace/v2"
)
```

#### [包名](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E5%8C%85%E5%90%8D) <a href="#bao-ming" id="bao-ming"></a>

定义包名请遵循以下规范:

* 全部小写, 不要使用大写或下划线或其他特殊符号
* 大多数使用命名导入的情况下，不需要重命名
* 包名尽量简单而有含义，方便记忆和引用
* 不要使用复数，例如`net/url`，而不是`net/urls`。
* 不要用“common”，“util”，“shared”或“lib”这些是不好的，信息量不足的名称

#### [函数名](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E5%87%BD%E6%95%B0%E5%90%8D) <a href="#han-shu-ming" id="han-shu-ming"></a>

* 函数名使用驼峰命名法，不要使用下划线分隔单词 (部分测试函数可以使用下划线分隔单词)
* 函数名应该尽可能的描述函数的功能，不要使用无意义的名称

#### [函数的排序](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E5%87%BD%E6%95%B0%E7%9A%84%E6%8E%92%E5%BA%8F) <a href="#han-shu-de-pai-xu" id="han-shu-de-pai-xu"></a>

函数的排序应遵循以下规范：

* 函数的定义应该尽量按照调用顺序排序
* 同一个文件中函数应放在 `struct`, `const`, `var` 定义之后
* 有接收者的函数中的 `new` 或 `New` 开头的函数应放在前面

| 不推荐                                                                                                                                                                                                                                                     | 推荐                                                                                                                                                                                                                                                      |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <pre><code>func (s *something) Cost() {
  return calcCost(s.weights)
}

type something struct{ ... }

func calcCost(n []int) int {...}

func (s *something) Stop() {...}

func newSomething() *something {
    return &#x26;something{}
}
</code></pre> | <pre><code>type something struct{ ... }

func newSomething() *something {
    return &#x26;something{}
}

func (s *something) Cost() {
  return calcCost(s.weights)
}

func (s *something) Stop() {...}

func calcCost(n []int) int {...}
</code></pre> |

#### [减少嵌套](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E5%87%8F%E5%B0%91%E5%B5%8C%E5%A5%97) <a href="#jian-shao-qian-tao" id="jian-shao-qian-tao"></a>

代码应该有限处理错误或者特殊情况并且尽早返回，而不是嵌套代码块。可以使代码更直观简洁。

| 不推荐                                                                                                                                                                                                                               | 推荐                                                                                                                                                                                                          |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <pre><code>for _, v := range data {
  if v.F1 == 1 {
    v = process(v)
    if err := v.Call(); err == nil {
      v.Send()
    } else {
      return err
    }
  } else {
    log.Printf("Invalid v: %v", v)
  }
}
</code></pre> | <pre><code>for _, v := range data {
  if v.F1 != 1 {
    log.Printf("Invalid v: %v", v)
    continue
  }

  v = process(v)
  if err := v.Call(); err != nil {
    return err
  }
  v.Send()
}
</code></pre> |

#### [减少不必要的 else](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E5%87%8F%E5%B0%91%E4%B8%8D%E5%BF%85%E8%A6%81%E7%9A%84-else) <a href="#jian-shao-bu-bi-yao-de-else" id="jian-shao-bu-bi-yao-de-else"></a>

| 不推荐                                                                     | 推荐                                                  |
| ----------------------------------------------------------------------- | --------------------------------------------------- |
| <pre><code>var a int
if b {
  a = 100
} else {
  a = 10
}
</code></pre> | <pre><code>a := 10
if b {
  a = 100
}
</code></pre> |

#### [顶层变量声明](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E9%A1%B6%E5%B1%82%E5%8F%98%E9%87%8F%E5%A3%B0%E6%98%8E) <a href="#ding-ceng-bian-liang-sheng-ming" id="ding-ceng-bian-liang-sheng-ming"></a>

| 不推荐                                                                                                                                                                                                                                                                 | 推荐                                                                                                                                                          |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <pre><code>var _s string = F()

func F() string { return "A" }
</code></pre>                                                                                                                                                                                        | <pre><code>var _s = F()
// 由于 F 已经明确了返回一个字符串类型，
// 因此我们没有必要显式指定_s 的类型

func F() string { return "A" }
</code></pre>                                         |
| <p>如果我们希望 <code>_e</code> 为 <code>error</code> 类型， 以下定义是错误的, <code>_e</code> 会被定义为 <code>myError</code> 类型</p><pre><code>type myError struct{}

func (myError) Error() string { return "error" }

func F() myError { return myError{} }

var _e = F()
</code></pre> | <pre><code>type myError struct{}

func (myError) Error() string { return "error" }

func F() myError { return myError{} }

var _e error = F()
</code></pre> |

#### [对于未导出的顶层常量和变量使用 `_` 作为前缀](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E5%AF%B9%E4%BA%8E%E6%9C%AA%E5%AF%BC%E5%87%BA%E7%9A%84%E9%A1%B6%E5%B1%82%E5%B8%B8%E9%87%8F%E5%92%8C%E5%8F%98%E9%87%8F%E4%BD%BF%E7%94%A8-%E4%BD%9C%E4%B8%BA%E5%89%8D%E7%BC%80) <a href="#dui-yu-wei-dao-chu-de-ding-ceng-chang-liang-he-bian-liang-shi-yong-zuo-wei-qian-zhui" id="dui-yu-wei-dao-chu-de-ding-ceng-chang-liang-he-bian-liang-shi-yong-zuo-wei-qian-zhui"></a>

| Bad                                                                                       | Good                                                                                        |
| ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| <pre><code>// foo.go

const (
  defaultPort = 8080
  defaultUser = "user"
)
</code></pre> | <pre><code>// foo.go

const (
  _defaultPort = 8080
  _defaultUser = "user"
)
</code></pre> |

#### [结构体中的嵌入式类型需放在顶部且用空行隔开](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E7%BB%93%E6%9E%84%E4%BD%93%E4%B8%AD%E7%9A%84%E5%B5%8C%E5%85%A5%E5%BC%8F%E7%B1%BB%E5%9E%8B%E9%9C%80%E6%94%BE%E5%9C%A8%E9%A1%B6%E9%83%A8%E4%B8%94%E7%94%A8%E7%A9%BA%E8%A1%8C%E9%9A%94%E5%BC%80) <a href="#jie-gou-ti-zhong-de-qian-ru-shi-lei-xing-xu-fang-zai-ding-bu-qie-yong-kong-hang-ge-kai" id="jie-gou-ti-zhong-de-qian-ru-shi-lei-xing-xu-fang-zai-ding-bu-qie-yong-kong-hang-ge-kai"></a>

| 不推荐                                                                         | 建议                                                                           |
| --------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| <pre><code>type Client struct {
  version int
  http.Client
}
</code></pre> | <pre><code>type Client struct {
  http.Client

  version int
}
</code></pre> |

嵌入式类型优缺点

优点：

* 代码简洁
* 可以直接访问嵌入类型的方法和字段
* 可以实现接口

缺点：

* 可能会导致外部包访问到未导出的字段和方法
* 会导入嵌入式方法的特殊零值
* 会暴露嵌入式类型的所有字段和方法，所有字段和方法都显示出来，不一定是我们想要的
* 会导致方法调用的不确定性，如果嵌入的类型有相同的方法，会导致调用的不确定性
* 给嵌入式类型的字段赋值不方便，会和其他嵌入式类型混合在一起，不容易区分

| 不推荐                                                                                                                                                                                                                                     | 推荐                                                                                                                                                                                                                                                                                       |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <pre><code>type A struct {
    // Bad: A.Lock() and A.Unlock() 现在可用
    // 不提供任何功能性好处，并允许用户控制有关 A 的内部细节。
    sync.Mutex
}
</code></pre>                                                                                                 | <pre><code>type countingWriteCloser struct {
    // Good: Write() 在外层提供用于特定目的，
    // 并且委托工作到内部类型的 Write() 中。
    io.WriteCloser
    count int
}
func (w *countingWriteCloser) Write(bs []byte) (int, error) {
    w.count += len(bs)
    return w.WriteCloser.Write(bs)
}
</code></pre> |
| <pre><code>type Book struct {
    // Bad: 指针更改零值的有用性
    io.ReadWriter
    // other fields
}
// later
var b Book
b.Read(...)  // panic: nil pointer
b.String()   // panic: nil pointer
b.Write(...) // panic: nil pointer
</code></pre> | <pre><code>type Book struct {
    // Good: 有用的零值
    bytes.Buffer
    // other fields
}
// later
var b Book
b.Read(...)  // ok
b.String()   // ok
b.Write(...) // ok
</code></pre>                                                                                                       |
| <pre><code>type Client struct {
    sync.Mutex
    sync.WaitGroup
    bytes.Buffer
    url.URL
}
</code></pre>                                                                                                                          | <pre><code>type Client struct {
    mtx sync.Mutex
    wg  sync.WaitGroup
    buf bytes.Buffer
    url url.URL
}
</code></pre>                                                                                                                                                           |

#### [nil 是一个有效的 slice](https://goguide.ryansu.tech/guide/standard/1-golang.html#nil-%E6%98%AF%E4%B8%80%E4%B8%AA%E6%9C%89%E6%95%88%E7%9A%84-slice) <a href="#nil-shi-yi-ge-you-xiao-de-slice" id="nil-shi-yi-ge-you-xiao-de-slice"></a>

当 `slice` 为 `nil` 时表示一个长度为 0 的切片

* 当返回切片为空时不应该返回一个空切片而是返回 `nil`

| 不推荐                                                    | 建议                                                 |
| ------------------------------------------------------ | -------------------------------------------------- |
| <pre><code>if x == "" {
return []int{}
}
</code></pre> | <pre><code>if x == "" {
return nil
}
</code></pre> |

* 使用 `len(s) == 0` 判断是否为空而不是 `s != nil`

| 不推荐                                                                        | 建议                                                                            |
| -------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| <pre><code>func isEmpty(s []string) bool {
return s == nil
}
</code></pre> | <pre><code>func isEmpty(s []string) bool {
return len(s) == 0
}
</code></pre> |

* 零值切片（用`var`声明的切片）可立即使用，无需调用`make()`创建

| 不推荐                                                                                                                                                 | 推荐                                                                                                                      |
| --------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| <pre><code>nums := []int{}
// or, nums := make([]int)

if add1 {
    nums = append(nums, 1)
}

if add2 {
    nums = append(nums, 2)
}
</code></pre> | <pre><code>var nums []int

if add1 {
    nums = append(nums, 1)
}

if add2 {
    nums = append(nums, 2)
}
</code></pre> |

#### [减少变量作用域](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E5%87%8F%E5%B0%91%E5%8F%98%E9%87%8F%E4%BD%9C%E7%94%A8%E5%9F%9F) <a href="#jian-shao-bian-liang-zuo-yong-yu" id="jian-shao-bian-liang-zuo-yong-yu"></a>

尽量减少变量作用域，除非变量在其他地方也被调用

| Bad                                                                                                                                                                                             | Good                                                                                                                                                                                                                                                |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <pre><code>err := os.WriteFile(name, data, 0644)
if err != nil {
 return err
}
</code></pre>                                                                                                    | <pre><code>if err := os.WriteFile(name, data, 0644); err != nil {
 return err
}
</code></pre>                                                                                                                                                       |
| <pre><code>if data, err := os.ReadFile(name); err == nil {
  err = cfg.Decode(data)
  if err != nil {
    return err
  }

  fmt.Println(cfg)
  return nil
} else {
  return err
}
</code></pre> | <p>由于 err 变量在 if 语句中声明，所以它的作用域仅限于 if 语句块。这样可以避免在 else 语句中使用相同的变量名。</p><pre><code>data, err := os.ReadFile(name)
if err != nil {
   return err
}

if err := cfg.Decode(data); err != nil {
  return err
}

fmt.Println(cfg)
return nil
</code></pre> |

#### [使用原生字符串而不是转义](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E4%BD%BF%E7%94%A8%E5%8E%9F%E7%94%9F%E5%AD%97%E7%AC%A6%E4%B8%B2%E8%80%8C%E4%B8%8D%E6%98%AF%E8%BD%AC%E4%B9%89) <a href="#shi-yong-yuan-sheng-zi-fu-chuan-er-bu-shi-zhuan-yi" id="shi-yong-yuan-sheng-zi-fu-chuan-er-bu-shi-zhuan-yi"></a>

当字符串内有转义字符时，优先使用 \` 来包裹字符串，表示这是原生字符串，不需要转义

| 不推荐                                                           | 推荐                                                           |
| ------------------------------------------------------------- | ------------------------------------------------------------ |
| <pre><code>wantError := "unknown name:\"test\""
</code></pre> | <pre><code>wantError := `unknown error:"test"`
</code></pre> |

#### [初始化结构体](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E5%88%9D%E5%A7%8B%E5%8C%96%E7%BB%93%E6%9E%84%E4%BD%93) <a href="#chu-shi-hua-jie-gou-ti" id="chu-shi-hua-jie-gou-ti"></a>

[**使用字段名初始化结构**](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E4%BD%BF%E7%94%A8%E5%AD%97%E6%AE%B5%E5%90%8D%E5%88%9D%E5%A7%8B%E5%8C%96%E7%BB%93%E6%9E%84)

初始化结构体赋值的时候尽量添加字段名，这样可以避免因为结构体字段的变化导致初始化错误

| Bad                                                     | Good                                                                                               |
| ------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| <pre><code>k := User{"John", "Doe", true}
</code></pre> | <pre><code>k := User{
    FirstName: "John",
    LastName: "Doe",
    Admin: true,
}
</code></pre> |

[**忽略 0 值的字段**](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E5%BF%BD%E7%95%A5-0-%E5%80%BC%E7%9A%84%E5%AD%97%E6%AE%B5)

若初始化的字段为默认的 0 值，可以省略字段名

| 不推荐                                                                                                                | 推荐                                                                               |
| ------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------- |
| <pre><code>user := User{
  FirstName: "John",
  LastName: "Doe",
  MiddleName: "",
  Admin: false,
}
</code></pre> | <pre><code>user := User{
  FirstName: "John",
  LastName: "Doe",
}
</code></pre> |

[**若初始化全为 0 值的结构变量，使用 `var`**](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E8%8B%A5%E5%88%9D%E5%A7%8B%E5%8C%96%E5%85%A8%E4%B8%BA-0-%E5%80%BC%E7%9A%84%E7%BB%93%E6%9E%84%E5%8F%98%E9%87%8F-%E4%BD%BF%E7%94%A8-var)

| 不推荐                                     | 推荐                                     |
| --------------------------------------- | -------------------------------------- |
| <pre><code>user := User{}
</code></pre> | <pre><code>var user User
</code></pre> |

[**初始化结构体指针**](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E5%88%9D%E5%A7%8B%E5%8C%96%E7%BB%93%E6%9E%84%E4%BD%93%E6%8C%87%E9%92%88)

初始化结构体指针时，使用 `&` 符号， 而不是 `new()`

| 不推荐                                                       | 推荐                                                    |
| --------------------------------------------------------- | ----------------------------------------------------- |
| <pre><code>sptr := new(T)
sptr.Name = "bar"
</code></pre> | <pre><code>sptr := &#x26;T{Name: "bar"}
</code></pre> |

[**使用 `make()` 初始化 map**](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E4%BD%BF%E7%94%A8-make-%E5%88%9D%E5%A7%8B%E5%8C%96-map)

如果初始化 `map`, 如果 `map` 有初始值，建议使用 `:=` 而不是 `make()`，如果没有初始值，使用 `make()`，且建议估计 `map` 大小，设置初始化容量

| 不推荐                                                                               | 推荐                                                                       |
| --------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| <pre><code>m := make(map[T1]T2, 3)
m[k1] = v1
m[k2] = v2
m[k3] = v3
</code></pre> | <pre><code>m := map[T1]T2{
  k1: v1,
  k2: v2,
  k3: v3,
}
</code></pre> |
| <pre><code>m := make(map[T1]T2)
</code></pre>                                     | <pre><code>m := make(map[T1]T2， 3)
</code></pre>                         |

#### [若在 Printf 外定义 format 字符串，建议使用 const](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E8%8B%A5%E5%9C%A8-printf-%E5%A4%96%E5%AE%9A%E4%B9%89-format-%E5%AD%97%E7%AC%A6%E4%B8%B2-%E5%BB%BA%E8%AE%AE%E4%BD%BF%E7%94%A8-const) <a href="#ruo-zai-printf-wai-ding-yi-format-zi-fu-chuan-jian-yi-shi-yong-const" id="ruo-zai-printf-wai-ding-yi-format-zi-fu-chuan-jian-yi-shi-yong-const"></a>

如果在 `Printf` 外定义格式化字符串，建议使用 `const` 常量，这样可以避免重复定义格式化字符串, 且可以帮助 `go vet` 进行静态分析。

| Bad                                                                                | Good                                                                                    |
| ---------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| <pre><code>msg := "unexpected values %v, %v\n"
fmt.Printf(msg, 1, 2)
</code></pre> | <pre><code>const msg = "unexpected values %v, %v\n"
fmt.Printf(msg, 1, 2)
</code></pre> |

### [开发原则](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E5%BC%80%E5%8F%91%E5%8E%9F%E5%88%99) <a href="#kai-fa-yuan-ze" id="kai-fa-yuan-ze"></a>

#### [error 处理](https://goguide.ryansu.tech/guide/standard/1-golang.html#error-%E5%A4%84%E7%90%86) <a href="#error-chu-li" id="error-chu-li"></a>

[**错误类型**](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E9%94%99%E8%AF%AF%E7%B1%BB%E5%9E%8B)

错误类型通常有两种：

* 静态类型： 由 `errors.New()` 创建的错误类型，通常用于预定义的错误, 错误信息不变
* 动态类型: 由 `fmt.Errorf()` 创建的或者自定义的错误类型，通常用于动态错误信息

错误匹配

当判断错误类型时，不要使用 `==` 进行比较，应该使用 `errors.Is()` 或者 `errors.As()` 进行比较，且应该创建顶级错误变量用于判断

```
// package foo
var ErrCouldNotOpen = errors.New("could not open")

func Open() error {
  return ErrCouldNotOpen
}

// package bar

if err := foo.Open(); err != nil {
  if errors.Is(err, foo.ErrCouldNotOpen) {
    // handle the error
  } else {
    panic("unknown error")
  }
}
```

[**错误包装**](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E9%94%99%E8%AF%AF%E5%8C%85%E8%A3%85)

我们可以使用 `fmt.Errorf()` 或者 `errors.Wrap()` 来包装错误，这样可以保留原始错误信息，同时添加额外的上下文信息

注意

`fmt.Errorf()` 在 Go 1.13 之后，可以使用 `%w` 格式化符号来包装错误，这样可以使用 `errors.Is()` 和 `errors.As()` 来判断错误类型， 如果使用 `%v` 格式化符号，会丢失错误类型信息，导致无法使用 `errors.Is()` 和 `errors.As()` 来判断错误类型。

```
s, err := store.New()
if err != nil {
    return fmt.Errorf(
        "new store: %w", err)
}
```

[**错误命名**](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E9%94%99%E8%AF%AF%E5%91%BD%E5%90%8D)

普通错误变量的命名应该以 `Err` 开头，后面跟错误的描述，使用驼峰命名法

```
var (
  // 导出以下两个错误，以便此包的用户可以将它们与 errors.Is 进行匹配。

  ErrBrokenLink = errors.New("link is broken")
  ErrCouldNotOpen = errors.New("could not open")

  // 这个错误没有被导出，因为我们不想让它成为我们公共 API 的一部分。 我们可能仍然在带有错误的包内使用它。

  errNotFound = errors.New("not found")
)
```

自定义的错误命名则建议使用 `Error` 作为后缀

```
// 同样，这个错误被导出，以便这个包的用户可以将它与 errors.As 匹配。

type NotFoundError struct {
  File string
}

func (e *NotFoundError) Error() string {
  return fmt.Sprintf("file %q not found", e.File)
}

// 并且这个错误没有被导出，因为我们不想让它成为公共 API 的一部分。 我们仍然可以在带有 errors.As 的包中使用它。
type resolveError struct {
  Path string
}

func (e *resolveError) Error() string {
  return fmt.Sprintf("resolve %q", e.Path)
}
```

[**依次处理错误**](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E4%BE%9D%E6%AC%A1%E5%A4%84%E7%90%86%E9%94%99%E8%AF%AF)

在处理错误时, 我们应该使用 `errors.Is()` 和 `errors.As()` 来判断错误类型，根据不同的错误类型进行不同的处理，如果错误无法处理，则应该明确返回错误可以来源，方便上级处理。

| 描述                                                                                                                                                | 代码                                                                                                                                                                                                                                      |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>不推荐</strong>: 记录错误并将其返回</p><p>堆栈中的调用程序可能会对该错误采取类似的操作。这样做会在应用程序日志中造成大量噪音，但收效甚微。</p>                                                     | <pre><code>u, err := getUser(id)
if err != nil {
  // BAD: See description
  log.Printf("Could not get user %q: %v", id, err)
  return err
}
</code></pre>                                                                              |
| <p><strong>推荐</strong>: 将错误换行并返回</p><p>堆栈中更靠上的调用程序将处理该错误。使用<code>%w</code>可确保它们可以将错误与<code>errors.Is</code>或<code>errors.As</code>相匹配 （如果相关）。</p> | <pre><code>u, err := getUser(id)
if err != nil {
  return fmt.Errorf("get user %q: %w", id, err)
}
</code></pre>                                                                                                                        |
| <p><strong>推荐</strong>: 记录错误并正常降级</p><p>如果操作不是绝对必要的，我们可以通过从中恢复来提供降级但不间断的体验。</p>                                                                   | <pre><code>if err := emitMetrics(); err != nil {
  // Failure to write metrics should not
  // break the application.
  log.Printf("Could not emit metrics: %v", err)
}
</code></pre>                                                   |
| <p><strong>推荐</strong>: 匹配错误并适当降级</p><p>如果被调用者在其约定中定义了一个特定的错误，并且失败是可恢复的，则匹配该错误案例并正常降级。对于所有其他案例，请包装错误并返回。</p><p>堆栈中更靠上的调用程序将处理其他错误。</p>            | <pre><code>tz, err := getUserTimeZone(id)
if err != nil {
  if errors.Is(err, ErrUserNotFound) {
    // User doesn't exist. Use UTC.
    tz = time.UTC
  } else {
    return fmt.Errorf("get user %q: %w", id, err)
  }
}
</code></pre> |

#### [类型断言](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E7%B1%BB%E5%9E%8B%E6%96%AD%E8%A8%80) <a href="#lei-xing-duan-yan" id="lei-xing-duan-yan"></a>

在我们需要类型断言的时候，务必使用 `ok` 返回值判断，否则会导致 `panic`

| 不推荐                                                   | 推荐                                                                   |
| ----------------------------------------------------- | -------------------------------------------------------------------- |
| <pre><code>t := i.(string) // 会导致 panic
</code></pre> | <pre><code>t, ok := i.(string)
if !ok {
  // 优雅地处理错误
}
</code></pre> |

#### [尽量不使用 `panic`](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E5%B0%BD%E9%87%8F%E4%B8%8D%E4%BD%BF%E7%94%A8-panic) <a href="#jin-liang-bu-shi-yong-panic" id="jin-liang-bu-shi-yong-panic"></a>

在生产环境中尽量不要使用 `panic`, `panic` 是 [级联失败](https://en.wikipedia.org/wiki/Cascading\_failure) 的主要原因，如果必须使用 `panic` ，务必使用 `recover()` 进行处理。

#### [使用 atomic 原子操作](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E4%BD%BF%E7%94%A8-atomic-%E5%8E%9F%E5%AD%90%E6%93%8D%E4%BD%9C) <a href="#shi-yong-atomic-yuan-zi-cao-zuo" id="shi-yong-atomic-yuan-zi-cao-zuo"></a>

在并发编程中，我们应该使用 `atomic` 包提供的原子操作来保证并发安全，可以保证基本类型如 `int32, int64` 在一个时刻只有一个 goroutine 可以访问。

对于其他类型，则推荐使用 `channel` 或 `sync lock` 进行控制

| 不推荐                                                                                                                                                                                                                                                                                   | 推荐                                                                                                                                                                                                                                                  |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <pre><code>type foo struct {
  running int32  // atomic
}

func (f* foo) start() {
  if atomic.SwapInt32(&#x26;f.running, 1) == 1 {
     // already running…
     return
  }
  // start the Foo
}

func (f *foo) isRunning() bool {
  return f.running == 1  // race!
}
</code></pre> | <pre><code>type foo struct {
  running atomic.Bool
}

func (f *foo) start() {
  if f.running.Swap(true) {
     // already running…
     return
  }
  // start the Foo
}

func (f *foo) isRunning() bool {
  return f.running.Load()
}
</code></pre> |

#### [不要在公共的结构中使用嵌入类型](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E4%B8%8D%E8%A6%81%E5%9C%A8%E5%85%AC%E5%85%B1%E7%9A%84%E7%BB%93%E6%9E%84%E4%B8%AD%E4%BD%BF%E7%94%A8%E5%B5%8C%E5%85%A5%E7%B1%BB%E5%9E%8B) <a href="#bu-yao-zai-gong-gong-de-jie-gou-zhong-shi-yong-qian-ru-lei-xing" id="bu-yao-zai-gong-gong-de-jie-gou-zhong-shi-yong-qian-ru-lei-xing"></a>

不要在公共的结构中使用嵌入类型， 主要原因是如果嵌入多个类型，则会导致大量公开接口和变量混杂，不好管理和配置，且相同的变量和函数可能冲突。且无法保证后续的版本不会冲突。

| 不推荐                                                                                            | 推荐                                                                                                                                                                                                                                                         |
| ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <pre><code>// ConcreteList 是一个实体列表。
type ConcreteList struct {
  *AbstractList
}
</code></pre> | <pre><code>// ConcreteList 是一个实体列表。
type ConcreteList struct {
  list *AbstractList
}
// 添加将实体添加到列表中。
func (l *ConcreteList) Add(e Entity) {
  l.list.Add(e)
}
// 移除从列表中移除实体。
func (l *ConcreteList) Remove(e Entity) {
  l.list.Remove(e)
}
</code></pre> |

#### [避免使用内置名称](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E9%81%BF%E5%85%8D%E4%BD%BF%E7%94%A8%E5%86%85%E7%BD%AE%E5%90%8D%E7%A7%B0) <a href="#bi-mian-shi-yong-nei-zhi-ming-cheng" id="bi-mian-shi-yong-nei-zhi-ming-cheng"></a>

声明变量的时候应避免使用内置的名称，如 `len`, `cap`, `append`, `copy`, `new`, `make`, `close`, `delete`, `complex`, `real`, `imag`, `panic`, `recover`, `print`, `println`, `error`, `string`, `int`, `uint`, `uintptr`, `byte`, `rune`, `float32`, `float64`, `bool`, `true`, `false`, `iota`, `nil`, `true`, `false`, `iota`, `nil`, `append`, `cap`, `close`, `complex`, `copy`, `delete`, `imag`, `len`, `make`, `new`, `panic`, `print`, `println`, `real`, `recover`, `string`, `uint`, `uintptr`, `byte`, `rune`, `float32`, `float64`, `int`, `int8`, `int16`, `int32`, `int64`, `uint`, `uint8`, `uint16`, `uint32`, `uint64`, `uintptr`, `bool` 等

#### [避免使用 `init` 函数](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E9%81%BF%E5%85%8D%E4%BD%BF%E7%94%A8-init-%E5%87%BD%E6%95%B0) <a href="#bi-mian-shi-yong-init-han-shu" id="bi-mian-shi-yong-init-han-shu"></a>

`init` 函数是在包被导入的时候自动执行的，但是由于 `init` 函数的执行顺序是不确定的，所以在 `init` 函数中初始化的变量可能会导致不确定的结果，所以尽量避免使用 `init` 函数。

什么时候要用 \`init()\`

* 当导入包需要赋值的过程十分复杂，且表达式不能用单个变量赋值时
* 使用可插入的钩子函数如 `database/sql` 时
* 对某些预计算方法进行初始化优化

#### [提前配置 slice 的容量](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E6%8F%90%E5%89%8D%E9%85%8D%E7%BD%AE-slice-%E7%9A%84%E5%AE%B9%E9%87%8F) <a href="#ti-qian-pei-zhi-slice-de-rong-liang" id="ti-qian-pei-zhi-slice-de-rong-liang"></a>

若能提前知道大概得数据量，应提前给 `slice` 配置容量，减少 `slice` 扩容的次数，提高性能。

| 不推荐                                                                                                                                                  | 推荐                                                                                                                                                         |
| ---------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <pre><code>for n := 0; n &#x3C; b.N; n++ {
  data := make([]int, 0)
  for k := 0; k &#x3C; size; k++{
    data = append(data, k)
  }
}
</code></pre> | <pre><code>for n := 0; n &#x3C; b.N; n++ {
  data := make([]int, 0, size)
  for k := 0; k &#x3C; size; k++{
    data = append(data, k)
  }
}
</code></pre> |
| <pre><code>BenchmarkBad-4    100000000    2.48s
</code></pre>                                                                                        | <pre><code>BenchmarkGood-4   100000000    0.21s
</code></pre>                                                                                              |

#### [使用 Exit 或 Fatal 退出主程序](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E4%BD%BF%E7%94%A8-exit-%E6%88%96-fatal-%E9%80%80%E5%87%BA%E4%B8%BB%E7%A8%8B%E5%BA%8F) <a href="#shi-yong-exit-huo-fatal-tui-chu-zhu-cheng-xu" id="shi-yong-exit-huo-fatal-tui-chu-zhu-cheng-xu"></a>

在主程序中，如果遇到错误，应该使用 `os.Exit` 或 `log.Fatal` 退出程序，而不是使用 `panic`，因为 `panic` 会导致程序崩溃，而 `os.Exit` 或 `log.Fatal` 会正常退出程序。且应该将错误传递到最终的调用者，而不是在每个函数中处理致命错误。

相关信息

最好**仅在**`main()` 中调用其中一个 `os.Exit` 或者 `log.Fatal*`。所有其他函数应将错误返回到 `main` 主程序中。

原因：

* 太多函数可以调用 `Fatal` 的话会导致难以控制程序流
* `Fatal` 错误可能导致 `test` 无法全部执行
* `Fatal` 错误可能导致 `defer` 无法执行

| Bad                                                                                                                                                                                                                                                                                  | Good                                                                                                                                                                                                                                                                                                                                             |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <pre><code>func main() {
  body := readFile(path)
  fmt.Println(body)
}
func readFile(path string) string {
  f, err := os.Open(path)
  if err != nil {
    log.Fatal(err)
  }
  b, err := os.ReadAll(f)
  if err != nil {
    log.Fatal(err)
  }
  return string(b)
}
</code></pre> | <pre><code>func main() {
  body, err := readFile(path)
  if err != nil {
    log.Fatal(err)
  }
  fmt.Println(body)
}
func readFile(path string) (string, error) {
  f, err := os.Open(path)
  if err != nil {
    return "", err
  }
  b, err := os.ReadAll(f)
  if err != nil {
    return "", err
  }
  return string(b), nil
}
</code></pre> |

#### [在序列化的结构体中需声明 Tag](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E5%9C%A8%E5%BA%8F%E5%88%97%E5%8C%96%E7%9A%84%E7%BB%93%E6%9E%84%E4%BD%93%E4%B8%AD%E9%9C%80%E5%A3%B0%E6%98%8E-tag) <a href="#zai-xu-lie-hua-de-jie-gou-ti-zhong-xu-sheng-ming-tag" id="zai-xu-lie-hua-de-jie-gou-ti-zhong-xu-sheng-ming-tag"></a>

在序列化的结构体中，应该声明 `json` 或 `xml` 等序列化的 `tag`，以便序列化和反序列化时能够正确的解析数据。

| 推荐                                                                                                                                            | 不推荐                                                                                                                                                                                                               |
| --------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <pre><code>type Stock struct {
  Price int
  Name  string
}
bytes, err := json.Marshal(Stock{
  Price: 137,
  Name:  "UBER",
})
</code></pre> | <pre><code>type Stock struct {
  Price int    `json:"price"`
  Name  string `json:"name"`
  // Safe to rename Name to Symbol.
}
bytes, err := json.Marshal(Stock{
  Price: 137,
  Name:  "UBER",
})
</code></pre> |

#### [注意协程 goroutine 的使用](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E6%B3%A8%E6%84%8F%E5%8D%8F%E7%A8%8B-goroutine-%E7%9A%84%E4%BD%BF%E7%94%A8) <a href="#zhu-yi-xie-cheng-goroutine-de-shi-yong" id="zhu-yi-xie-cheng-goroutine-de-shi-yong"></a>

注意

在使用协程时，应该注意以下几点：

* goroutine 的数量应该受限制，避免无限制的创建 goroutine
* goroutine 必须有一个可预测的停止时间
* goroutine 必须有停止的方法

| Bad                                                                                    | Good                                                                                                                                                                                                                                                                                                                                                                                                                          |
| -------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <pre><code>go func() {
  for {
    flush()
    time.Sleep(delay)
  }
}()
</code></pre> | <pre><code>var (
  stop = make(chan struct{}) // 告诉 goroutine 停止
  done = make(chan struct{}) // 告诉我们 goroutine 退出了
)
go func() {
  defer close(done)
  ticker := time.NewTicker(delay)
  defer ticker.Stop()
  for {
    select {
    case &#x3C;-tick.C:
      flush()
    case &#x3C;-stop:
      return
    }
  }
}()
// 其它...
close(stop)  // 指示 goroutine 停止
&#x3C;-done       // and wait for it to exit
</code></pre> |
| 没有办法阻止这个 goroutine。这将一直运行到应用程序退出。                                                      | 这个 goroutine 可以用 `close(stop)`, 我们可以等待它退出 `<-done`.                                                                                                                                                                                                                                                                                                                                                                           |

[**等待 goroutines 退出**](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E7%AD%89%E5%BE%85-goroutines-%E9%80%80%E5%87%BA)

在 goroutine 执行时，需要使用函数保证主程序不退出，否则会终止 goroutine 的执行。

有两种常用的方法可以做到这一点：

*   使用 `sync.WaitGroup`. 如果您要等待多个 goroutine，请执行此操作

    ```
    var wg sync.WaitGroup
    for i := 0; i < N; i++ {
      wg.Add(1)
      go func() {
        defer wg.Done()
        // ...
      }()
    }

    // To wait for all to finish:
    wg.Wait()
    ```
*   添加另一个 `chan struct{}`，goroutine 完成后会关闭它。 如果只有一个 goroutine，请执行此操作。

    ```
    done := make(chan struct{})
    go func() {
      defer close(done)
      // ...
    }()

    // To wait for the goroutine to finish:
    <-done
    ```

#### [不要在 `init()` 中使用 `goroutine`](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E4%B8%8D%E8%A6%81%E5%9C%A8-init-%E4%B8%AD%E4%BD%BF%E7%94%A8-goroutine) <a href="#bu-yao-zai-init-zhong-shi-yong-goroutine" id="bu-yao-zai-init-zhong-shi-yong-goroutine"></a>

在 `init()` 函数中使用 `goroutine` 会导致程序的初始化变得复杂，因为 `init()` 函数是在程序启动时执行的，而 `goroutine` 是异步执行的，可能会导致程序的初始化顺序变得不确定。

### [性能优化](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E6%80%A7%E8%83%BD%E4%BC%98%E5%8C%96) <a href="#xing-neng-you-hua" id="xing-neng-you-hua"></a>

#### [优先使用 strconv 而不是 fmt](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E4%BC%98%E5%85%88%E4%BD%BF%E7%94%A8-strconv-%E8%80%8C%E4%B8%8D%E6%98%AF-fmt) <a href="#you-xian-shi-yong-strconv-er-bu-shi-fmt" id="you-xian-shi-yong-strconv-er-bu-shi-fmt"></a>

在进行字符串转换时，尽量使用 `strconv` 包，而不是 `fmt` 包，因为 `fmt` 包是比较重的，而 `strconv` 包是比较轻的。`strconv` 包转换速度更快，所需资源更少。

#### [指定 map, slice 的容量](https://goguide.ryansu.tech/guide/standard/1-golang.html#%E6%8C%87%E5%AE%9A-map-slice-%E7%9A%84%E5%AE%B9%E9%87%8F) <a href="#zhi-ding-mapslice-de-rong-liang" id="zhi-ding-mapslice-de-rong-liang"></a>

如果提前知道大概容量，请提前赋值，以避免不必要的内存分配和自动扩容。

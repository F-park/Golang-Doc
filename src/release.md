# 更新日志

**最新版本：**

- `go1.21.5`，发布于2023-12-05

- `go.1.20.12`，发布于2023-12-05

**维护版本：**

- `go1.21` 发布于2023-08-08
- `go1.20` 发布于2023-02-01

<br>

Go官方采用语义化版本来标识更新，格式为v`主版本`.`次版本`.`补丁版本` （见[语义化版本 2.0.0 | Semantic Versioning (semver.org)](https://semver.org/lang/zh-CN/)），主版本的更新意味着发生了Breaking Change，即无法向下兼容的更新，此版本的更新意味着有新功能添加同时保持向下兼容，补丁版本的更新意味着有问题被修复同时保持向下兼容。

Go2.0上一次提出草案是在2018年11月19日，那时还是处于go1.13版本，五年过后，版本已经迭代到了go1.21，Go2.0的各种想法已经通过增量更新的方式体现在了Go1.0上，创始人之一也曾明确表示未来可能并不会有Go2.0，Go将一直为保持向下兼容而努力（见[Go 1 and the Future of Go Programs - The Go Programming Language](https://go.dev/doc/go1compat)）。

Go团队每半年发布一个二级版本，并且只有最新的两个二级版本是长期维护，维护时间都是六个月，鉴于Go每一次更新都保持着相当高的兼容性，建议在新版本稳定后及时将Go升级到最新版。

Go语言官方更新日志：[Release History - The Go Programming Language](https://go.dev/doc/devel/release)

::: tip

此页面只是对官方日志的一个简单搬运，不定期更新，想获取最新消息还请前往官网。

:::



## 1.21

Go1.21更新日志：[Release History - The Go Programming Language](https://go.dev/doc/devel/release#go1.21.0)

### 1.21.0 （2023-08-08）

**语言层面**

1. 新增了两个内置函数`min` ，`max`，用于计算最大值最小值。
2. 新增内置函数`clear`，用于清空map和slice
3. 更新了`package`初始化顺序

    - 按导入路径对所有包进行排序
    - 重复执行，直到包的列表为空
    - 找到列表中所有的导入都已被初始化的第一个包
    - 初始化该包并将其从列表中删除

4. 提高和改进了类型推理的能力和精度，主要是泛型相关。

5. 推出了`for range`循环变量改进的预览版本，这是一个困扰了Go开发者接近十年的问题，官方终于要解决了，详情见：[LoopvarExperiment · golang/go Wiki (github.com)](https://github.com/golang/go/wiki/LoopvarExperiment)和[Proposal: Less Error-Prone Loop Variable Scoping (googlesource.com)](https://go.googlesource.com/proposal/+/master/design/60078-loopvar.md)

6. 保证了`recover`的返回值不会是`nil`，如果在调用`panic`时参数为`nil`，则会触发另一个`panic`，返回`*runtime.PanicNilError`。为了兼容性，在编译时设置`GODEBUG=panicnil=1`允许向`panic`传入`nil`。

**标准库**

1. 新增`log/slog`库，提供标准的结构化日志库
2. 新增`testing/slogtest`库，用于验证`slog.Handler`的实现
3. 新增`slices`库，提供了一系列泛型函数用于操作切片。
4. 新增`maps`库，提供了一系列泛型函数用于操作map
5. 新增`cmp`库，用于比较有序类型。

**其他**

1. go1.21.0至少在windows系统上至少需要win10或者Windows Server 2016版本以上才能运行，先前的版本不再支持。
2. go1.21.0至少需要在macOS 10.15 Catalina或者更新的版本才能运行，先前的版本不再支持。
3. 新增了实验性的WebAssembly System Interface，Go依旧在WASM这块不断的探索。
4.  在1.20还是实验性质的（Profile-guide optimization）PGO（见[Profile-guided optimization - The Go Programming Language](https://go.dev/doc/pgo)），1.21版本正式启用。在main包下包含`default.pgo`文件会启用该功能，开启后性能可能会提升2%-7%。
5. 当打印非常深的运行时调用栈时，从原来的只打印前一百个帧，到现在分别打印前50的最后的50个帧。
6. 优化了在Unix平台CGO的调用性能，从1-3微秒优化到了现在的100-200纳秒。
7. 在1.21版本，编译速度提升了接近6%，这主要归功于编译器本身使用PGO来构建。

以上是一些主要的更新信息，更多内容请访问[Go 1.21 Release Notes - The Go Programming Language](https://go.dev/doc/go1.21#introduction)



### 1.21.1（2023-09-06）

1. 修复了`cmd/go`, `crypto/tls`,  `html/template` 包的安全问题
2. 修复了编译器，go命令行, linker, runtime, 以及包 `context`, `crypto/tls`, `encoding/gob`, `encoding/xml`, `go/types`, `net/http`, `os`,`path/filepath`的一些bug。

更多细节前往：[1.21.1 Issues · golang/go (github.com)](https://github.com/golang/go/issues?q=milestone%3AGo1.21.1+label%3ACherryPickApproved)



### 1.21.2（2023-10-05）

1. 修复了`cmd/go`包的安全问题
2. 修复了编译器, go命令行,linker,runtime,  以及包`runtime/metrics`的一些bug。 

更多细节前往：[1.21.2 Issues · golang/go (github.com)](https://github.com/golang/go/issues?q=milestone%3AGo1.21.2+label%3ACherryPickApproved)



### 1.21.3（2023-10-10）

1. 修复了`net/http`包关于http2中handler的协程数量最大值的问题。


更多细节前往：[1.21.3 Issues · golang/go (github.com)](https://github.com/golang/go/issues?q=milestone%3AGo1.21.3+label%3ACherryPickApproved)



### 1.21.4（2023-11-07）

1. 修复了`path/filepath`的有关于解析windows路径的安全问题。
2. 修复了`linker`，`compiler`，`runtime`，`http`，`cgo`的一些bug。

更多细节前往：[1.21.4 Issues · golang/go (github.com)](https://github.com/golang/go/issues?q=milestone%3AGo1.21.4+label%3ACherryPickApproved)



### 1.21.5（2023-12-05）

1. 修复了命令行和`net/http`，`path/filepath`的安全问题
2. 修复了 compiler, go command, the runtime, 以及包 `crypto/rand`, `net`, `os`,  `syscall` 的一些bug。

更多细节前往：[1.21.5 Issues · golang/go (github.com)](https://github.com/golang/go/issues?q=milestone%3AGo1.21.5+label%3ACherryPickApproved)



## 1.20

Go1.20更新日志：[1.20 Release History - The Go Programming Language](https://go.dev/doc/devel/release#go1.20)

### 1.20.0 （2023-02-01）

**语言层面**

1. 在将切片类型转换为数组时，原来需要对指针数组解引用`*(*[4byte])(x)`来避免和切片操作同一个底层数组，现在可以直接这么写`[4]byte(x)`。
2. `unsafe`新增了`SliceData`，`String`，`StringData`函数，用于构建和结构切片与字符串值。

**标准库**

1. 新增`crypto/ecdh`库，提供了对于ECDH（Elliptic Curve Diffie-Hellman，一种非对称加密方法）的支持。
2. go1.20扩展了对error包装的支持，允许一个error包装多个error。
3. 新增`net/http.ResponseContorller`，提供了一种更清晰、更易于发现的方法来添加每个handler controls。
4. `httputil.ReverseProxy`包含了一个新的Rewrite Hook函数，用于取代之前的Director Hook。

**其他**

1. go1.20是最后一个支持win7，8，Server2008和Server2012的版本，在未来版本中不再提供支持。
2. go1.20是最后一个支持macOS 10.13或10.14的版本，未来版本将不再提供支持。
3. 在1.18和1.19版本中，由于泛型的出现，相较于1.17编译速度出现了倒退，go1.20编译速度将会提升10%左右。
4. 发布PGO（Profile-guided optimization）的预览版本，这是一种计算机界的编译器优化技术，可以提高运行时性能。
5. 在go1.20，在没有C toolchains的系统上，go command禁用cgo。
6. 支持收集程序代码覆盖率文件，见[Coverage profiling support for integration tests - The Go Programming Language](https://go.dev/testing/coverage/)
7. 对GC进行了改进，提高了稳定性，减少内存开销，提升了整体2%的CPU性能。

以上是一些主要的更新信息，更多内容请访问[Go 1.20 Release Notes - The Go Programming Language](https://go.dev/doc/go1.20#introduction)



### 1.20.1 （2023-02-14）

1. 修复了一些库的安全问题

    - `crypto/tls`

    - `mime/multipart`

    - `net/http`

    - `path/filepath`
 2. 修复了编译器，go command，linker，runtime，time包的一些bug。

更多细节前往[1.20.1 Issues · golang/go (github.com)](https://github.com/golang/go/issues?q=milestone%3AGo1.20.1+label%3ACherryPickApproved)



### 1.20.2 （2023-03-07）

1. 修复了`crypto/elliptic`库的安全问题
2. 修复了编译器，covdata命令，linker，runtime，`crypto/ecdh`, `crypto/rsa`, `crypto/x509`, `os`, `syscall`库的一些bug

 更多细节前往[1.20.2 Issues · golang/go (github.com)](https://github.com/golang/go/issues?q=milestone%3AGo1.20.2+label%3ACherryPickApproved)



### 1.20.3 （2023-04-04）

1. 修复了以下库的安全问题
    - `go/parser`
    - `html/tempalte`
    - `mime/multipart`
    - `net/http`
    - `net/textproto`
2. 修复了编译器，linker，runtime，time包的bug

更多细节前往[1.20.3 Issues · golang/go (github.com)](https://github.com/golang/go/issues?q=milestone%3AGo1.20.3+label%3ACherryPickApproved)



### 1.20.4 （2023-05-02）

1. 修复了`html/tempalte`的三个安全问题
2. 修复了编译器，runtime，还有`crypto/subtle`, `crypto/tls`, `net/http`, `syscall`的一些bug。

更多细节前往[1.20.4 Issues · golang/go (github.com)](https://github.com/golang/go/issues?q=milestone%3AGo1.20.4+label%3ACherryPickApproved)



### 1.20.5 （2023-06-06）

1. 修复了四个来自`cmd/go`和`runtime`库的安全问题
2. 修复了编译器，go command，runtime，还有  `crypto/rsa`, `net`,  `os` 库的bug

更多细节前往[1.20.5 Issues · golang/go (github.com)](https://github.com/golang/go/issues?q=milestone%3AGo1.20.5+label%3ACherryPickApproved)



### 1.20.6 （2023-07-11）

1. 修复了来自`net/http`库的的安全问题（Host Header的校验问题，这个问题曾导致了Docker Engine API 无法正常使用，笔者曾经遇到过，见[Golang client fails to attach to streams with "http: invalid Host header" with go1.20.6, go1.19.11 · Issue #45935 · moby/moby (github.com)](https://github.com/moby/moby/issues/45935)）
2. 修复了编译器，cgo，cover tool，go command，runtime，还有`crypto/ecdsa`, `go/build`, `go/printer`, `net/mail`, `text/template` 库的一些bug。

更多细节前往[1.20.6 Issues · golang/go (github.com)](https://github.com/golang/go/issues?q=milestone%3AGo1.20.6+label%3ACherryPickApproved)



### 1.20.7 （2023-08-01）

1. 修复了`crypto/tls`库的安全问题
2. 修复了assembler，编译器的bug。

更多细节前往[1.20.7 Issues · golang/go (github.com)](https://github.com/golang/go/issues?q=milestone%3AGo1.20.7+label%3ACherryPickApproved)



### 1.20.8 （2023-09-06）

1. 修复了`html/template`包的两个安全问题
2. 修复了编译器，命令行，运行时以及 `crypto/tls`, `go/types`, `net/http`,  `path/filepath` 包的一些bug

更多细节前往[1.20.8 Issues · golang/go (github.com)](https://github.com/golang/go/issues?q=milestone%3AGo1.20.8+label%3ACherryPickApproved)



### 1.20.9 （2023-10-05）

1. 修复了`cmd/go`的一个安全问题
2. 修复了命令行，链接器的一些bug。

更多细节前往[1.20.9 Issues · golang/go (github.com)](https://github.com/golang/go/issues?q=milestone%3AGo1.20.9+label%3ACherryPickApproved)



### 1.20.10（2023-10-10）

修复了`net/http`包的一个安全问题，是关于http2中handler的协程数量最大值的问题。

更多细节前往：[1.20.10 Issues · golang/go (github.com)](https://github.com/golang/go/issues?q=milestone%3AGo1.20.10+label%3ACherryPickApproved)



### 1.20.11（2023-11-07）

1. 修复了`path/filepath`的有关于解析windows路径的安全问题。
2. 修复了linker，以及包`net/http`的bug。

更多细节前往：[1.20.11 Issues · golang/go (github.com)](https://github.com/golang/go/issues?q=milestone%3AGo1.20.11+label%3ACherryPickApproved)



### 1.20.12（2023-12-05）

1. 修复了命令行和`net/http`，`path/filepath`的安全问题
2. 修复了 compiler, go command的一些bug。

更多细节前往：[1.20.12 Issues · golang/go (github.com)](https://github.com/golang/go/issues?q=milestone%3AGo1.20.12+label%3ACherryPickApproved)



## 1.19

Go1.19更新日志：[Go 1.19 Release Notes - The Go Programming Language](https://go.dev/doc/go1.19)



## 1.18

GO1.18更新日志：[Go 1.18 Release Notes - The Go Programming Language](https://go.dev/doc/go1.18)



## 1.17

Go1.17更新日志：[Go 1.17 Release Notes - The Go Programming Language](https://go.dev/doc/go1.17)



## 1.16

Go1.16更新日志：[Go 1.16 Release Notes - The Go Programming Language](https://go.dev/doc/go1.16)




## 1.15

Go1.15更新日志：[Go 1.14 Release Notes - The Go Programming Language](https://go.dev/doc/go1.15)



## 1.14

Go1.14更新日志：[Go 1.14 Release Notes - The Go Programming Language](https://go.dev/doc/go1.14)



## 1.13

Go1.13更新日志：[Go 1.13 Release Notes - The Go Programming Language](https://go.dev/doc/go1.13)



## 1.12

Go1.12更新日志：[Go 1.12 Release Notes - The Go Programming Language](https://go.dev/doc/go1.12)



## 1.11

Go1.11更新日志：[Go 1.11 Release Notes - The Go Programming Language](https://go.dev/doc/go1.11)



## 1.10

Go1.10更新日志：[Go 1.10 Release Notes - The Go Programming Language](https://go.dev/doc/go1.10)



## 1.9（2017-08-24）

Go1.9更新日志：[Go 1.9 Release Notes - The Go Programming Language](https://go.dev/doc/go1.9)

## 1.8（2017-02-16）

Go1.8更新日志：[Go 1.8 Release Notes - The Go Programming Language](https://go.dev/doc/go1.8)

## 1.7（2016-08-15）

Go1.8更新日志：[Go 1.7 Release Notes - The Go Programming Language](https://go.dev/doc/go1.7)

## 1.6（2016-02-17）

Go1.6更新日志：[Go 1.6 Release Notes - The Go Programming Language](https://go.dev/doc/go1.6)

## 1.5（2015-8-19）

Go1.5更新日志：[Go 1.5 Release Notes - The Go Programming Language](https://go.dev/doc/go1.5)

## 1.4（2014-12-10）

Go1.4更新日志：[Go 1.4 Release Notes - The Go Programming Language](https://go.dev/doc/go1.4)

## 1.3（2014-06-18）

Go1.3更新日志：[Go 1.3 Release Notes - The Go Programming Language](https://go.dev/doc/go1.3)

## 1.2（2013-12-01）

Go1.2更新日志：[Go 1.2 Release Notes - The Go Programming Language](https://go.dev/doc/go1.2)

## 1.1（2013-05-12）

Go1.1更新日志：[Go 1.1 Release Notes - The Go Programming Language](https://go.dev/doc/go1.1)



**语言层面**：

1. 一个数被0整除以前会抛出`panic`，到了1.1直接无法通过编译。
2. 方法可以作为一个值存在。
3. 引入了终止语句的概念，函数的返回规则更为宽松。

**性能方面**：

1. 使用go1.1的工具编译的go程序性能大概可以提升30%-40%



## 1.0（2012-03-28）

Go1.0更新日志：[Go 1.0 Release Notes - The Go Programming Language](https://go.dev/doc/go1.0)





## pre

在go1正式发布之前，所有的版本都被称为预览版本，对于这些预览版本官方会每周发布一个快照版本，其中比较重要的版本有

- r60（2011-09-07），规定了else块现在必须加括号
- r59（2011-08-01），设计了新的结构体tag方案
- r58（2011-06-29），修复了滥用goto而导致内存未初始化的问题，新增了gui，exec包
- r57（2011-05-03），支持短变量多重赋值语法，重新设计了http，reflect包，将gotest作为一个go程序而非shell脚本
- r56（2011-03-07），第一个稳定版本

预览版本的开发始于2009年12月09日，在go1于2012年3月28日正式发布之后停止，持续了接近三年的时间，往后不再记录每周快照版本。前往[Pre-Go 1 Release History](https://go.dev/doc/devel/pre_go1)了解这些主要版本的信息，前往[Weekly Snapshot History](https://go.dev/doc/devel/weekly#2012-03-27)了解全部预览版本的每周快照版本信息。




# 02-入门

## 写一个程序

1. 打开命令行并cd到主目录

在 Linux 或 Mac 上：&#x20;

```sh
cd
```

在 Windows 上：

```bash
cd %HOMEPATH%
```

2. 使用以下命令为你的第一个 Go 源代码创建一个 hello 目录：

```bash
mkdir hello
cd hello
```

3. 启动依赖跟踪

当你的代码导入其他模块依赖时，你可以通过 module 管理这些依赖项。module 由 go.mod 文件定义，该文件负责跟踪依赖。 go.mod 文件与您的代码一起保留，包含在源代码存储库中。

要通过创建 go.mod 文件来启用代码的依赖项跟踪，请运行[`go mod init`命令](https://go.dev/ref/mod#go-mod-init)，并为其指定代码所在模块的名称。

在实际开发中，模块路径通常是保存源代码的存储库位置。例如，模块路径可能是`github.com/mymodule`

本教程由于是教学目的，下面就使用`example/hello`   来演示。

```bash
$ go mod init example/hello
go: creating new go.mod: module example/hello
```

4. 在文本编辑器中，创建一个文件 hello.go&#x20;

```go
package main
// 声明一个main包,你必须在源文件中非注释的第一行指明这个文件属于哪个包
// 如：package main。package main表示一个可独立执行的程序
// 每个 Go 应用程序都包含一个名为 main 的包。

// 导入fmt包，告诉 Go 编译器这个程序需要使用 fmt 包（的函数，或其他元素）
// fmt 包实现了格式化 IO（输入/输出）的函数。
import "fmt"

// 程序主入口,main 函数是每一个可执行程序所必须包含的
// 一般来说都是在启动后第一个执行的函数（如果有 init() 函数则会先执行该函数）。
func main() {
    fmt.Println("Hello, World!")
}
```

5. 运行你的代码查看程序输出

```go
$ go run .
Hello, World!
```

## 调用外部包中的代码

如何使用其他人写好的包，你可以访问 pkg.go.dev 并搜索“quote”包。

<figure><img src="../.gitbook/assets/截屏2024-08-05 17.19.22.png" alt=""><figcaption></figcaption></figure>

1. 在您的 Go 代码中，导入`rsc.io/quote`包并添加调用 到它的`Go`函数。

```go
package main

import "fmt"

import "rsc.io/quote"

func main() {
    fmt.Println(quote.Go())
}
```

2. 添加新的 module 和 sums

当您运行`go mod tidy`时，它会找到并下载包含您导入的包的`rsc.io/quote`模块。默认情况下，它下载的是最新版本

```bash
$ go mod tidy
go: finding module for package rsc.io/quote
go: found rsc.io/quote in rsc.io/quote v1.5.2
```

3. 运行您的代码以查看您正在调用的函数生成的消息。

```bash
$ go run .
Don't communicate by sharing memory, share memory by communicating.
```


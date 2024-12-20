# 01-环境准备

## 1. go 前世今生

Go 和 C语言、C++、Python、Java 等一样都是编程语言。Go 语言的创始人有三位，分别是图灵奖获得者、C 语法联合发明人、Unix 之父肯·汤普森（Ken Thompson），Plan 9 操作系统领导者、UTF-8 编码的最初设计者罗伯·派克（Rob Pike），以及 Java 的 HotSpot 虚拟机和 Chrome 浏览器的 JavaScript V8 引擎的设计者之一罗伯特·格瑞史莫（Robert Griesemer）。

他们可能都没有想到，他们三个人在 2007 年 9 月 20 日下午的一次普通讨论，就这么成为了计算机编程语言领域的一次著名历史事件，开启了一个新编程语言的历史。

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

那天下午，在谷歌山景城总部的那间办公室里，罗伯·派克启动了一个 C++ 工程的编译构建。按照以往的经验判断，这次构建大约需要一个小时。利用这段时间，罗伯·派克和罗伯特·格瑞史莫、肯·汤普森坐在一处，交换了关于设计一门新编程语言的想法。

之所以有这种想法，是**因为当时的谷歌内部主要使用 C++ 语言构建各种系统，但 C++ 的巨大复杂性、编译构建速度慢以及在编写服务端程序时对并发支持的不足**，让三位大佬觉得十分不便，他们就想着设计一门新的语言。在他们的初步构想中，这门新语言应该是能够给程序员带来快乐、匹配未来硬件发展趋势并适合用来开发谷歌内部大规模网络服务程序的。

在第一天的简短讨论后，第二天这三位大佬又在谷歌总部的“雅温得（Yaounde）”会议室里具体讨论了这门新语言的设计。会后罗伯特·格瑞史莫发出了一封题为“prog lang discussion”的电邮，对这门新编程语言的功能特性做了初步的归纳总结：

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

这封电邮对这门新编程语言的功能特性做了归纳总结。主要思路是，**在 C 语言的基础上，修正一些明显的缺陷，删除一些被诟病较多的特性，增加一些缺失的功能**，比如:

* 使用import替代include。
* 去掉宏（macro）。
* 理想情况是用一个源文件替代.h和.c文件，模块的接口应该被自动提取出来（而无须手动在.h文件中声明）。
* 语句像C语言一样，但需要修正switch语句的缺陷。
* 表达式像C语言一样，但有一些注意事项（比如是否需要逗号表达式）。
* 基本上是强类型的，但可能需要支持运行时类型。
* 数组应该总是有边界检查。
* 具备垃圾回收的机制。
* 支持接口（interface）。
* 支持嵌套和匿名函数/闭包。
* 一个简单的编译器。
* 各种语言机制应该能产生可预测的代码。

这封电邮成为了这门新语言的第一版特性设计稿，三位大佬在这门语言的一些基础语法特性上达成了初步一致。

2007年 9 月 25 日，罗伯·派克在一封回复电邮中把这门新编程语言命名为“go”：



<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

在罗伯·派克的心目中，“go”这个单词短小、容易输入并且在组合其他字母后便可以用来命名 Go 相关的工具，比如编译器（goc）、汇编器（goa）、链接器（gol）等（go 的早期版本曾如此命名 go 工具链，但后续版本撤销了这种命名方式，仅保留 go 这一统一的工具链名称 ）。



2009 年 10 月 30 日，罗伯·派克在 Google Techtalk 上做了一次有关 Go 语言的演讲“The Go Programming Language”，这也是 Go 语言第一次公之于众。十天后，也就是 2009 年 11 月 10 日，谷歌官方宣布 Go 语言项目开源，之后这一天也被 Go 官方确定为 Go 语言的诞生日。

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Go 语言发展得非常迅猛,从正式开源到现在，十二年的时间过去了，Go 语言发布了多个大版本更新，逐渐成熟。这里，我也梳理了迄今为止 Go 语言的重大版本更新，希望能帮助你快速了解 Go 语言的演化历史。

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

## 2. 安装 go 编译器

{% embed url="https://go.dev/doc/install" %}

选择相应操作系统的安装包下载，下载完成后双击安装包并按照提示进行安装。下面以 mac 电脑为例：

该安装包将 Go 安装到 /usr/local/go 目录下，并将 /usr/local/go/bin 目录放入`PATH`环境变量中。

mac 系统可以运行以下命令将 bin 文件放到 PATH 中，一般不需要我们手动操作：

```bash
export PATH=/usr/local/go/bin:$PATH
```

<figure><img src="../.gitbook/assets/截屏2024-08-05 16.54.52.png" alt=""><figcaption></figcaption></figure>

安装完成后，在终端输入以下指令，检查是否安装成功。

```bash
$ go version
// go version go1.22.3 darwin/arm64 
```

## 3. 开发工具

* go playground 【在线学习】 [https://go.dev/play/](https://go.dev/play/)  纯小白推荐，学习语言用
* goland 【收费】 [https://www.jetbrains.com/go/](https://www.jetbrains.com/go/) 需要激活码，激活码可以去淘宝购买，30块钱左右
* vscode 【免费】 [https://code.visualstudio.com/](https://code.visualstudio.com/)  免费使用，新手推荐





####

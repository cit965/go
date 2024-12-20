# 05-数据类型和变量

## 什么是类型

```bash
bool
Numeric Types
int8, int16, int32, int64, int
uint8, uint16, uint32, uint64, uint
float32, float64
complex64, complex128
byte
rune
string
```

#### 布尔类型 <a href="#boolean_types" id="boolean_types"></a>

`true`和`false`

#### 数字类型 <a href="#numeric_types" id="numeric_types"></a>

_整数_、_浮&#x70B9;_&#x6216;_复&#x6570;_&#x7C7B;型分别表示整数、浮点或复数值的集合。它们统称&#x4E3A;_&#x6570;字类型_

```go
uint8       the set of all unsigned  8-bit integers (0 to 255)
uint16      the set of all unsigned 16-bit integers (0 to 65535)
uint32      the set of all unsigned 32-bit integers (0 to 4294967295)
uint64      the set of all unsigned 64-bit integers (0 to 18446744073709551615)

int8        the set of all signed  8-bit integers (-128 to 127)
int16       the set of all signed 16-bit integers (-32768 to 32767)
int32       the set of all signed 32-bit integers (-2147483648 to 2147483647)
int64       the set of all signed 64-bit integers (-9223372036854775808 to 9223372036854775807)

float32     the set of all IEEE-754 32-bit floating-point numbers
float64     the set of all IEEE-754 64-bit floating-point numbers

complex64   the set of all complex numbers with float32 real and imaginary parts
complex128  the set of all complex numbers with float64 real and imaginary parts

byte        alias for uint8
rune        alias for int32
```

#### 字符串类型 <a href="#string_types" id="string_types"></a>



```go
package main

import "fmt"

func main() {
	// 整型
	fmt.Println(666)
	fmt.Println(6 + 9)
	fmt.Println(6 - 9)
	fmt.Println(6 * 9)
	fmt.Println(16 / 9) // 商
	fmt.Println(16 % 9) // 余数

	// 字符串类型，特点：通过双引号
	fmt.Println("南哥")
	fmt.Println("南哥" + "666")
	// 对比
	fmt.Println("1" + "2") // 结果："12"
	fmt.Println(1 + 2)     // 结果：3

	// 布尔类型，真假
	fmt.Println(1 > 2) // false  假
	fmt.Println(1 < 2) // true   真


}
```

## 什么是变量 <a href="#shen-me-shi-bian-liang" id="shen-me-shi-bian-liang"></a>

变量是指定存储特定类型值的内存位置的名称，可以理解为昵称。在 Go 中声明变量有多种语法。我们一个一个来看。

### 声明变量（不初始化）

var name type 是声明单个变量的语法

```go
package main

import "fmt"

func main() {  
    var age int // variable declaration
    fmt.Println("My age is", age)
}
```

语句 var age int 声明了一个名为 age 的 int 类型变量。我们没有给这个变量赋任何值。如果一个变量没有分配任何值，Go 会自动将其初始化为该变量类型的零值。在本例中，age 被赋值为0，即 int 的零值。如果运行此程序，可以看到以下输出:

```go
My age is 0 
```

可以将变量赋给其类型的任何值。在上面的程序中，年龄可以分配任何整数值。

```go
package main

import "fmt"

func main() {  
    var age int // variable declaration
    fmt.Println("My age is", age)
    age = 29 //assignment
    fmt.Println("My age is", age)
    age = 54 //assignment
    fmt.Println("My new age is", age)
}
```

上面的程序将打印以下输出。

```go
My age is  0  
My age is 29  
My new age is 54 
```

### 声明变量（初始化） <a href="#sheng-ming-ju-you-chu-shi-zhi-de-bian-liang" id="sheng-ming-ju-you-chu-shi-zhi-de-bian-liang"></a>

声明变量时，还可以提供初始值。下面是用初始值声明变量的语法。

```go
var name type = initialvalue  
```

```go
package main

import "fmt"

func main() {  
    var age int = 29 // variable declaration with initial value

    fmt.Println("My age is", age)
}
```

在上面的程序中，age 是 int 类型的变量，初始值为29。上面的程序将打印以下输出。

```go
My age is 29  
```

### 先声明后赋值

```go
// 声明了一个int类型变量 age
var age int
// 给 age 变量赋值
age = 21
fmt.Println(sd)
```

### 类型推断 <a href="#lei-xing-tui-duan" id="lei-xing-tui-duan"></a>

如果一个变量有一个初始值，Go 将能够使用该初始值自动推断该变量的类型。因此，如果变量具有初始值，则可以删除变量声明中的类型。如果使用以下语法声明变量，Go 将从初始值自动推断该变量的类型。

```go
package main
import "fmt"

func main() {  
    // 在下面的示例中，我们可以看到在第6行中删除了变量 age 的 int 类型。
    // 由于变量的初始值为29，Go 可以推断它的类型为 int。
    var age = 29 // type will be inferred
    fmt.Println("My age is", age)
}
```

### 多变量声明 <a href="#duo-bian-liang-sheng-ming" id="duo-bian-liang-sheng-ming"></a>

可以使用单个语句声明多个变量。 var name1，name2 type = initialvalue1，initialvalue2是多变量声明的语法。

```go
package main

import "fmt"

func main() {  
    var width, height int = 100, 50 //declaring multiple variables

    fmt.Println("width is", width, "height is", height)
}
```

在某些情况下，我们可能希望在一个语句中声明属于不同类型的变量，这叫做块声明。下面的程序使用上述语法声明不同类型的变量。

```go
package main

import "fmt"

func main() {  
    var (
        name   = "naveen"
        age    = 29
        height int
    )
    fmt.Println("my name is", name, ", age is", age, "and height is", height)
}
```

#### 简短声明 <a href="#jian-duan-sheng-ming" id="jian-duan-sheng-ming"></a>

go 还提供了另一种声明变量的简洁方法。这称为简写声明，它使用: = 操作符。

name: = initialvalue 是声明变量的简写语法。

下面的程序使用简短语法来声明初始化为10的变量计数。Go 将自动推断 count 的类型为 int，因为它是用整数值10初始化的。

```go
package main

import "fmt"

func main() {  
    count := 10
    fmt.Println("Count =",count)
}
```

还可以使用简短的语法在一行中声明多个变量,下面的程序分别声明了 string 和 int 类型的两个变量 name 和 age。

```go
package main

import "fmt"

func main() {  
    name, age := "naveen", 29 //short hand declaration

    fmt.Println("my name is", name, "age is", age)
}
```

只有当: = 左侧的至少一个变量是新声明的时候，才能使用简短语法。考虑下面的程序

```go
package main

import "fmt"

func main() {  
    a, b := 20, 30 //a and b declared
    fmt.Println("a is", a, "b is", b)
    a, b := 40, 50 //error, no new variables
}
```

它会打印 `error/pro.go: 8:10: 在 := 的左边没有新变量` , 这是因为变量 a 和 b 都已经声明过了，在第8行 := 的左边没有新变量

# 变量

```go
package main

import "fmt"

var c, python, java bool

func main() {
	var i int
	fmt.Println(i, c, python, java)
}
```

var 用于定义一系列变量，可以定义在 package 下和 func 下，定义的方式与 func 参数定义一致，类型放在变量之后

### 添加默认值

```go
var i, j int = 1, 2
var c, python, java = true, false, "no!"
```

定义默认值的时候可以不定义类型，go 会依据默认值的类型来限制变量

变量定义过类型（添加默认值后），就不能修改其类型、赋值其他类型的值了

当没有设默认值时，数字类型默认为 0，布尔值默认为 false，字符串默认为 “”



### := 初始化操作符

:= 可以替代 var 初始化变量，上面的例子可以改成如下

```go
i, j := 1, 2
c, python, java := true, false, "no!"
```

**注意**

:= 操作符只能在 func 中使用，不能在 package 下使用（var 可以）



## 常量

```go
const Pi = 3.14

func main() {
	const World = "世界"
	fmt.Println("Hello", World)
	fmt.Println("Happy", Pi, "Day")

	const Truth = true
	fmt.Println("Go rules?", Truth)
}
```

常量不能用 `:=` 定义
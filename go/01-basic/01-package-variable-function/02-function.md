# 函数

### 参数和返回值需要有类型定义

函数的参数和返回值需要有类型定义

```go
func add(x int, y int) int {
	return x + y
}
```

当前面参数与后面参数一致时，可以省略前面参数的类型

```go
func add(x, y int) int { // 这里 x 的类型被省略了，说明 x 和 y 一样都是 int
	return x + y
}
```



### 多参数返回

```go
package main

import "fmt"

func swap(x, y string) (string, string) {
	return y, x
}

func main() {
	a, b := swap("hello", "world")
	fmt.Println(a, b)
}
```

支持一次性返回多个参数到新的变量中

有多少个返回参数，也就需要有多少个变量去接收返回值



### 定义返回变量（不推荐哦）

```go
func split(sum int) (x, y int) {
	x = sum * 4 / 9
	y = sum - x
	return
}
```

return 后没写任何内容，将依据返回值里定义的变量去返回，这里将会返回 x y




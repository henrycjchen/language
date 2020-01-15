# array 数组

声明：`var a [10]int`

例子

```go
func main() {
	var a [2]string
	a[0] = "Hello"
	a[1] = "World"
	fmt.Println(a[0], a[1])
	fmt.Println(a)

	primes := [6]int{2, 3, 5, 7, 11, 13}
	fmt.Println(primes)
}
```



## slice

数组切割，按指定的范围切割数组，返回新数组，而**不影响**原数组

语法：`a[low : high]`

- low 省略时表示从头开始

- high 活力时表示到末尾结束
- low 和 high 都省略时（冒号 `:` 不能省略）表示复制数组
- 新数组里的元素是原数组的引用，修改新数组时也**会修改**原数组

例子一

```go
func main() {
	primes := [6]int{2, 3, 5, 7, 11, 13}

	var s []int = primes[1:4]
	fmt.Println(s)
}
```

例子二：修改新数组

```go
func main() {
	names := [4]string{
		"John",
		"Paul",
		"George",
	}
	fmt.Println(names)

	a := names[0:2]
	b := names[1:3]
	fmt.Println(a, b)

	b[0] = "XXX"
	fmt.Println(a, b)
	fmt.Println(names)
}
```



## 长度 len 和容量 cap

长度表示数组现有元素的个数

容量表示数组实有元素的个数

```go
func main() {
	s := []int{2, 3, 5, 7, 11, 13}
	printSlice(s) // len=6 cap=6 [2 3 5 7 11 13]

	// Slice the slice to give it zero length.
	s = s[:0]
	printSlice(s) // len=0 cap=6 []

	// Extend its length.
	s = s[:4]
	printSlice(s) // len=4 cap=6 [2 3 5 7]

	// Drop its first two values.
	s = s[2:]
	printSlice(s) // len=2 cap=4 [5 7]
}

func printSlice(s []int) {
	fmt.Printf("len=%d cap=%d %v\n", len(s), cap(s), s)
}
```

当 slice 的 high 索引小于长度时，len 会变小，但 cap 不变，数据可”还原“

当 slice 的 low 索引大于 0 时，会修改到容量 cap，数据不可”还原“



## 空数组 == nil

```go
func main() {
	var s []int
	fmt.Println(s, len(s), cap(s)) // [] 0 0
	if s == nil { // true
		fmt.Println("nil!") // nil!
	}
}
```



## make 初始化数组

```go
func main() {
	a := make([]int, 5)
	printSlice("a", a)

	b := make([]int, 0, 5)
	printSlice("b", b)

	c := b[:2]
	printSlice("c", c)

	d := c[2:5]
	printSlice("d", d)
}

func printSlice(s string, x []int) {
	fmt.Printf("%s len=%d cap=%d %v\n",
		s, len(x), cap(x), x)
}
```

内置函数 make 可以初始化数组的元素类型、长度和容量



## 二维数组

```go
package main

import (
	"fmt"
	"strings"
)

func main() {
	// Create a tic-tac-toe board.
	board := [][]string{
		[]string{"_", "_", "_"},
		[]string{"_", "_", "_"},
		[]string{"_", "_", "_"},
	}

	// The players take turns.
	board[0][0] = "X"
	board[2][2] = "O"
	board[1][2] = "X"
	board[1][0] = "O"
	board[0][2] = "X"

	for i := 0; i < len(board); i++ {
		fmt.Printf("%s\n", strings.Join(board[i], " "))
	}
}
```



## append 添加元素

```go
func main() {
	var s []int
	printSlice(s) // len=0 cap=0 []

	// append works on nil slices.
	s = append(s, 0) // len=1 cap=2 [0]
	printSlice(s)

	// The slice grows as needed.
	s = append(s, 1) // len=2 cap=2 [0 1]
	printSlice(s)

	// We can add more than one element at a time.
    a := append(s, 2, 3, 4) // len=5 cap=8 [0 1 2 3 4]
    a[0] = 1
	printSlice(a)
    printSlice(s)
}

func printSlice(s []int) {
	fmt.Printf("len=%d cap=%d %v\n", len(s), cap(s), s)
}
```

- 当数组容量不够时，会创建一个拥有足够容量的**新数组**来存储新元素，出于效率考虑，新创建的数组容量会扩展一倍
- 新数组的修改**不会影响**到原数组
# range

数组循环

```go
var pow = []int{1, 2, 4, 8, 16, 32, 64, 128}

func main() {
	for i, v := range pow {
		fmt.Printf("2**%d = %d\n", i, v)
	}
}
```

第一个参数 i 表示数组索引，当不需要时可以用 `_` 表示省略

第二个参数 v 表示数组值，当不需要时可以用 `_` 表示省略，也可以不填

```go
func main() {
	pow := make([]int, 10)
	for i := range pow {
		pow[i] = 1 << uint(i) // == 2**i
	}
	for _, value := range pow {
		fmt.Printf("%d\n", value)
	}
}
```


# channel 通道

channel 是 goroutine 之间的通信机制

```go
func sum(s []int, c chan int) {
	sum := 0
	for _, v := range s {
		sum += v
	}
	c <- sum // send sum to c
}

func main() {
	s := []int{7, 2, 8, -9, 4, 0}

	c := make(chan int)
	go sum(s[:len(s)/2], c) // 17
	go sum(s[len(s)/2:], c) // -5
	x, y := <-c, <-c // receive from c

	fmt.Println(x, y, x+y) // -5 17 12
}
```

- goroutine 执行无序，所以这个 x y 是不能确定的

## 缓冲通道

```go
func main() {
	ch := make(chan int, 2)
	ch <- 1
	ch <- 2
	fmt.Println(<-ch)
	fmt.Println(<-ch)
}
```

通道支持配置缓冲大小，遵循先进先出

上例配了 2 个缓冲大小，支持往通道中放入两个值。

当放入的值大于缓冲大小，将会在运行时出现死锁

## 循环通道接收

```go
func fibonacci(n int, c chan int) {
	x, y := 0, 1
	for i := 0; i < n; i++ {
		c <- x
		x, y = y, x+y
	}
	close(c)
}

func main() {
	c := make(chan int, 10)
	go fibonacci(cap(c), c)
	for i := range c {
		fmt.Println(i)
	}
}
```

range 循环接收通道 c 内容，直到发送方关闭通道 `close(c)`

- close 命令只能由发送方发出


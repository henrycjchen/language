# goroutine

go 中，每一个并发执行的活动称为 goroutine。

```go
func main() {
	go spinner(100 * time.Millisecond)
	const n = 45
	fibN := fib(n)
	fmt.Printf("\rFibonacci(%d) = %d\n", n, fibN)
}

func spinner(delay time.Duration) {
	for {
		for _, r := range `-\|/` {
			fmt.Printf("\r%c", r)
			time.Sleep(delay)
		}
	}
}

func fib(x int) int {
	if x < 2 {
		return x
	}
	return fib(x-1) + fib(x-2)
}
```

这个例子中 spinner 和 fib 会同时执行，当 fib 结束，main 函数返回时，spinner 这个 goroutine 会暴力地直接终结
# defer 延迟函数调用

defer 是对函数或方法调用的一个声明，表示延迟调用该方法，直到所在函数执行结束（相当于给当前函数添加 after 方法）。

通常用于成对的操作，如打开&关闭、连接&断开、加锁&解锁，以保证资源在任何情况下能够正确释放。

### 例

```go
func title(url string) error {
    resp, err := http.Get(url)
    if err != nil {
        return err
    }
    
    ct := resp.Header.Get("Content-Type")
    if ct != "text/html" {
        resp.Body.Close()
        return fmt.Errorf("...")
    }
    
    doc, err := html.Parse(resp.Body)
    resp.Body.Close()
    ...
    return nil
}
```

上面这个例子，重复的 resp.Body.Close() 保证 title 函数在任何情况下都会关闭网络连接。这一重新的清理动作将会在条件复杂时变成难以维护。

下面用 defer 可以很好地处理这种问题

```go
func title(url string) error {
    resp, err := http.Get(url)
    if err != nil {
        return err
    }
    defer resp.Body.Close()
    
    ct := resp.Header.Get("Content-Type")
    if ct != "text/html" {
        return fmt.Errorf("...")
    }
    
    doc, err := html.Parse(resp.Body)
    ...
    return nil
}
```



### 注意

当多个 defer 调用存在时，遵循先进后出的堆栈原则，先 defer 定义的函数后执行

```go
func main() {
	fmt.Println("counting")

	for i := 0; i < 10; i++ {
		defer fmt.Println(i)
	}

	fmt.Println("done")
}
```


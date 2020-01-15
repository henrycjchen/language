# switch

```go
switch os := runtime.GOOS; os {
    case "darwin":
    fmt.Println("OS X.")
    case "linux":
    fmt.Println("Linux.")
    default:
    // freebsd, openbsd,
    // plan9, windows...
    fmt.Printf("%s.\n", os)
}
```

- 不需要写 break，case 匹配时只会执行当前 case 的代码



## 可以不写条件

```go
switch {
    case t.Hour() < 12:
    fmt.Println("Good morning!")
    case t.Hour() < 17:
    fmt.Println("Good afternoon.")
    default:
    fmt.Println("Good evening.")
}
```


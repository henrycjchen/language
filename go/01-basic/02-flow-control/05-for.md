# for 循环

```go
sum := 0
for i := 0; i < 10; i++ {
    sum += i
}
fmt.Println(sum)
```

- go 唯一的循环语法

- for 的三个语句都是可省略的

## for 当 while

```go
sum := 1
for sum < 1000 {
    sum += sum
}
fmt.Println(sum)
```

## for 无限循环

```go
for {
}
```


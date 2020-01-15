# method 方法

go 没有类 class，但可以给一个类型定义方法

```go
type Vertex struct {
	X, Y float64
}

func (v Vertex) Abs() float64 {
	return math.Sqrt(v.X*v.X + v.Y*v.Y)
}

func main() {
	v := Vertex{3, 4}
	fmt.Println(v.Abs())
}
```

这里给类型 Vertex 定义了方法 Abs，Abs 里可以直接使用类型 Vertex 的变量作为参数



## 给基础类型添加方法

```go
type MyFloat float64

func (f MyFloat) Abs() float64 {
	if f < 0 {
		return float64(-f)
	}
	return float64(f)
}

func main() {
	f := MyFloat(-math.Sqrt2)
	fmt.Println(f.Abs())
}
```

**注意**

方法不能直接添加在基础类型上，只能添加在自定义类型上



## 指针上的方法

可以直接通过指针修改 struct 上的属性

```go
type Vertex struct {
	X, Y float64
}

func (v Vertex) Abs() float64 {
	return math.Sqrt(v.X*v.X + v.Y*v.Y)
}

func (v *Vertex) Scale(f float64) {
	v.X = v.X * f
	v.Y = v.Y * f
}

func main() {
	v := Vertex{3, 4}
	v.Scale(10)
	fmt.Println(v.Abs())
}
```

Scale 是指针上的方法，但 `v.Scale(10)` 这样调用时，`v` 并不是指针呀，为什么还可以编译通过呢？

在 Go 中，为了方便，当方法有指针接收者时，Go 会自动把 `v` 解析成 `&v`。

当然你写成 `(&v).Scale(10)` 也是可以的

### 注意

如果自定义类型上任何一个方法使用指针接收者，建议该类型下所有的方法都使用指针接收者

好处：

1. 方便更新指针的值
2. 避免方法操作时复制这个结构体，当这个结构体特别大时，这个复制将使应用变得低效



## 实现 String 输出方法

给 Person 定义 String 方法后，fmt.Println 会调用这个方法实现输出

```go
type Person struct {
	Name string
	Age  int
}

func (p Person) String() string {
	return fmt.Sprintf("%v (%v years)", p.Name, p.Age)
}

func main() {
	a := Person{"Arthur Dent", 42}
	z := Person{"Zaphod Beeblebrox", 9001}
	fmt.Println(a, z)
}
```



## 实现 Error 输出方法

```go
type MyError struct {
	When time.Time
	What string
}

func (e *MyError) Error() string {
	return fmt.Sprintf("at %v, %s",
		e.When, e.What)
}

func run() error {
	return &MyError{
		time.Now(),
		"it didn't work",
	}
}

func main() {
	if err := run(); err != nil {
		fmt.Println(err)
	}
}
```


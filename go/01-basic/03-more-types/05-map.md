# map 散列表

空值为 `nil`

```go
type Vertex struct {
	Lat, Long float64
}

var m map[string]Vertex

func main() {
	m = make(map[string]Vertex)
	m["Bell Labs"] = Vertex{
		40.68433, -74.39967,
	}
	fmt.Println(m["Bell Labs"])
}
```



字面量声明

```go
type Vertex struct {
	Lat, Long float64
}

var m = map[string]Vertex{
	"Bell Labs": {40.68433, -74.39967},
	"Google":    {37.42202, -122.08408},
}

func main() {
	fmt.Println(m)
}
```



## 修改

```go
func main() {
	m := make(map[string]int)

	m["Answer"] = 42
	fmt.Println("The value:", m["Answer"])

	m["Answer"] = 48 // 修改
	fmt.Println("The value:", m["Answer"])

	delete(m, "Answer") // 删除
	fmt.Println("The value:", m["Answer"])

	v, ok := m["Answer"] // 获取、判断是否存在
	fmt.Println("The value:", v, "Present?", ok)
}
```
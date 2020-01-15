# 类型

## 基础类型

- bool
- string
- int    int8     int16    int32     int64
- uint  uint8  uint16  uint32  uint64
- byte - int8 的别名
- rune - int32 的别名，表示一个 unicode
- float32  float64
- complex64  complex128



### 注意

- string 字符串需要用双引号括起来
  - 当用单引号时，只能包裹一个字符，表示其对应的 Unicode int32 编码

## 类型转换

```go
var x, y int = 3, 4
var f float64 = math.Sqrt(float64(x*x + y*y))
var z uint = uint(f)
fmt.Println(x, y, z)
```

这里的转换指的是将变量 a 转换成另一个类型后赋值给变量 b，并不能直接修改变量 a 的类型

变量一被赋值的时候就定义了他的类型，后面将不能改变他的类型




## 引用

引用定义在 package 之下，func 之上

```go
package main

import (
	"fmt"
	"math/rand"
)

func main() {
	fmt.Println("My favorite number is", rand.Intn(10))
}

```

这里引用了 fmt 和 math 的子包 rand



也支持分别引用

```go
import "fmt"
import "math"
```



但第一种引用是更好的方式



### 包方法名

一个包中，大写开头的方法是公有方法，会被导出以外部调用，而小写开头的方法则不会被导出

```go
package main

import (
	"fmt"
	"math"
)

func main() {
	fmt.Println(math.pi) // p 小写，会报错
}
```


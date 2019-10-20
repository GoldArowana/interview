# 变量与常量
## 内建变量类型
- bool, string
- (u)int, (u)int8, (u)int16, (u)int32, (u)int64, uintptr
- byte, rune
- float32, float64, complex64, complex128

## 示例
### 1. 声明变量名、类型并赋予默认值
```go
var a int
var b int
fmt.Println(a, b)  // 0 0
```

### 2. 同类型变量可以定义在一行
```go
var a, b int = 3, 4
var c string = "hha"
fmt.Println(a, b, c) // 3 4 "hha"
```

### 3. 类型自动推断
```go
var a, b, c, d = 1, 2.2, true, "hha"
fmt.Println(a, b, c, d) // 1 2.2 true hha
```

### 4. 简短声明 :=
不过它有一个限制，那就是它只能用在函数内部；在函数外部使用则会无法编译通过，所以一般用var方式来定义全局变量
- [Golang - var 和 := 的使用](https://studygolang.com/articles/5294)
```go
a, b, c, d := 1, 2.2, true, "hha"
b = 3.3
fmt.Println(a, b, c, d) // 1 3.3 true hha
```

### 5. go语言支持复数
下面的1i就是复数部分
```go
fmt.Printf("%.3f\n", cmplx.Exp(1i*math.Pi)+1)
```

### 6. 全局变量
```go
var aa int
var bb = false
```

### 7. 可以将多个全局变量定义到一起
```go
var (
	cc = 3.3
	dd = 100
)
```

### 8. 常量
```go
const (
    happy = "hha"
    a, b  = 3, 4
)
fmt.Println(happy, math.Sqrt(a*a+b*b)) // hha 5
```


### 9. 借助iota定义常量
iota是从0开始，不断自增+1的一个数
```go
const (
    b = 1 << (10 * iota)
    kb
    mb
    gb
)
fmt.Println(b, kb, mb, gb) // 1 1024 1048576 1073741824
```

### 10. 借助_跳过iota的某一值
```go
const (
    apple = iota
    _
    banana
    lemon
)
fmt.Println(apple, banana, lemon) // 0 2 3
```

# 分支语句

## if语句

### go语言的if语句不用括号
```go
cmp := 100

if cmp > 1 {
    fmt.Println("ok")
}
```

### if语句里可以定义变量
上面示例中的cmp变量的定义部分也可以写在if里
```go
if cmp := 100; cmp > 1 {
    fmt.Println("ok")
}
```

### switch语句
go语言在switch里不用写break
```go
cmp := 100

switch cmp {
case 100:
    fmt.Println("一百")
case 200:
    fmt.Println("两百")
}
```

### switch语句内可以进行判断，而不必是常量
在switch里可以进行判断，如：score > 100 
```go
func grade(score int) string {
	g := ""
	switch {
	case score > 100 || score < 0:
		panic(fmt.Sprint("Wrong score : %maps", score))
	case score < 60:
		g = "F"
	case score < 80:
		g = "C"
	case score < 90:
		g = "B"
	case score <= 100:
		g = "A"
	}
	return g
}

func main() {
	fmt.Println(
		grade(10),
		grade(70),
		grade(80),
		grade(90),
	) // F C B A
}
```
# 循环语句

## go语言的for也是分为三段
```go
// 转为2进制
func convertToBin(n int) string {
	result := ""
	for ; n > 0; n /= 2 {
		result = strconv.Itoa(n%2) + result
	}
	return result
}

func main() {
	fmt.Println(convertToBin(13)) // 1101
}
```

### go语言的死循环
```go
for {
    fmt.Println("--------")
}
```

### go语言for语句代替while语句
示例：将变量s中的文本按行进行输出
```go
func printFileContent(reader io.Reader) {
	scanner := bufio.NewScanner(reader)
	for scanner.Scan() {
		fmt.Println(scanner.Text())
	}
}

func main() {
	s := `##########
ssdffaa34
fadsfa3442
##########`

	reader := strings.NewReader(s)
	printFileContent(reader)
}
```
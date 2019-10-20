# 正则表达式

## 示例
```go
const text = `
My email is haha@gmail.com
email2 is abc@def.com
email3 id ddd@qq.com
`

func main() {
	re := regexp.MustCompile("\\w+@\\w+\\.\\w+")
	match := re.FindAllString(text, -1)
	fmt.Println(match) // [haha@gmail.com abc@def.com ddd@qq.com]
}
```
# Enum in Go

Goには `enum` (列挙型)がない？ `const` を使って定義する。

const内で使用される[iota識別子](https://golang.org/ref/spec#Iota)は要素ごとに0からインクリメントしてくれる。

```go
package main

import "fmt"

type Direction int

const (
    NORTH = iota
    EAST
    SOUTH
    WEST    
)

func main() {
    fmt.Println(NORTH)
    fmt.Println(EAST)
    fmt.Println(SOUTH)
    fmt.Println(WEST)
}
```

実行すると…

```shell
$ go run main.go
0
1
2
3
```

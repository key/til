# Goのユニットテスト
## ディレクトリ構成

`sum.go` がロジックで `sum_test.go` がユニットテスト。

```text
.
└── src
    └── calc
        ├── sum.go
        └── sum_test.go
```

ユニットテスト用のファイルはsuffixに `_test` を付与し、 **メインのコードと同じ階層に配置** する。`go build`ではユニットテストのビルドが除外されるが、`go test` ではテストコードも含めてコンパイル・実行される。

> To write a new test suite, create a file whose name ends _test.go that contains the TestXxx functions as described here. Put the file in the same package as the one being tested. The file will be excluded from regular package builds but will be included when the “go test” command is run. For more detail, run “go help test” and “go help testflag”.
>
> 新しいテストスイートを作成するには、ここで説明するTestXxx関数を含む名前が_test.goで終わるファイルを作成します。 テスト対象のパッケージと同じパッケージにファイルを置きます。 ファイルは通常のパッケージビルドから除外されますが、 "go test"コマンドが実行されるとインクルードされます。 詳細については、 "go help test"と "help testflag"を実行してください。

## ファイルの中身

`sum.go`

```go:sum.go
package calc

func Sum(x int, y int) int {
	return x + y
}
```

ユニットテスト用の関数はprefixに `Test` を付与する（先に書いてある通り）。

`sum_test.go`

```go:sum_test.go
package calc

import "testing"

func TestSum(t *testing.T) {
	if Sum(1, 2) != 3 {
		t.Errorf("sum failed")
	}
}
```

## テスト実行

```shell
$ go test
PASS
ok  	_/Users/key/Documents/myProjects/go.geo/src/calc	0.007s
```

# 参考

- [Package testing](https://golang.org/pkg/testing/)
- [Golang basics - writing unit tests](http://blog.alexellis.io/golang-writing-unit-tests/)

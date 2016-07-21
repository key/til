# Swiftのcomputed property

2016/07/21

計算結果を返すプロパティ（computed propertyとかgetterのようなもの）が簡単に定義できる。
メソッドを呼び出す形ではないのでちょっと違和感があるが、短く書ける構文に見える。

構造体でもクラスでも同じように書けるっぽい。

```swift
struct SomeStruct {
    var unit = "mile"
    var distance: Float
    var computedDistance: Float {
        get {
            if unit == "mile" {
                return distance * 1.6
            } else {
                return distance
            }
        }
        set (newValue) {
            distance = newValue
        }
    }
}
```

playgroundで動かすとこんな感じ。

```swift
var s = SomeStruct(unit: "mile", distance: 100.0)

s.distance  // 100
s.computedDistance  // 160

s.unit = "meter" //
s.distance  // 100
s.computedDistance  // 100
```

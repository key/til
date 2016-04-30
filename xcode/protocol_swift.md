# Swiftでのプロトコル

2016/04/30

2行でまとめると、

- Optionalメソッドは定義できない（`@objc`付けると出来るけどSwiftらしくない）
- プロトコルとエクステンションを同時に定義すると良い

となる。

## プロトコル

```swift
public protocol HogeObservable: class {
    func didUpdateHoge(hoge: Hoge)
}
```

## エクステンション

```swift
extension HogeObservable {
    public func didUpdatedHoge(hoge: Hoge) {
        // 何も書かない
    }
}
```

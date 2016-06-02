# クラスを動的に読み出す

ビルドターゲット名とクラス名を繋げて`NSClassFromString()`を使って読み出す。
度のクラスかは事前に知っておく必要がありそう。

```objectivec
let className = "SourceAppName.SomeViewControllerOrClass"
let grabbedClass = NSClassFromString(className!) as! UIViewController.Type
let helloWorldClass = grabbedClass.init()
```

- [How to dynamically load class in swift?](http://stackoverflow.com/questions/35393527/how-to-dynamically-load-class-in-swift)
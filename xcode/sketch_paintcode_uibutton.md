# Sketch + PaintCode PluginでUIButton

2016/08/10

基底クラスを作って`hilighted`プロパティが更新されたら再描画するようにする。

```
class BaseButton: UIButton {
    override var highlighted: Bool {
        didSet {
            setNeedsDisplay()
        }
    }
}
```

`BaseButton`のサブクラスで`state`プロパティに応じたコードを呼び出す。

```
class PauseButton: BaseButton {
    override func drawRect(rect: CGRect) {
        if self.state == .Highlighted {
            StyleKit.drawPauseButtonHighlighted(frame: rect)
        } else {
            StyleKit.drawPauseButtonDefault(frame: rect)
        }
    }
}
```

## 課題

UIButtonは触った瞬間に少しだけアニメーションするのだが、
この実装だとアニメーションが消えてしまって違和感が残る。

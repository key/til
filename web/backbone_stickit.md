# backbone.stickit

2016/04/08

BackboneとStickitでMVVMする。段取りは次のような感じ。

- 前処理
    1. モデルを定義する
    2. ビューを定義する
        - セレクタとモデルの属性をマッピングする (`bindings`プロパティ)
    3. テンプレートを作る
        - ビューで定義したセレクタを含む要素を入れること
- 実処理
    1. テンプレートを描画する
    2. Stickitを呼び出す (`stickit()`)

## モデル

timestamp, messageという2つの属性を持つ想定。

```coffee
class TestModel extends Backbone.Model
  defaults:
    timestamp: null
    message: null
```

## テンプレート

timestamp, messageという2つの属性を持つ要素を定義する。

```html
<script type="text/template" id="tmpl-test">
    <h3 class="timestamp"></h3>
    <p class="message"></p>
</script>
```

## ビュー

テンプレートのHTMLは`tagName`で定義した要素に含められる。
`@stickit()`はテンプレートレンダリング後に呼び出すこと。

```coffee
class TestView etends Backbone.View
  tagName: 'div'
  model: TestModel
  template: _.template($("#tmpl-test").html())
  bindings:
    '.timestamp': 'timestamp'
    '.message': 'message'

  initialize: ->
    @render()

  render: ->
    @$el.html(@template({}))
    @stickit()
```

## 呼び出し

モデルを定義して、ビューに渡す。

```coffee
model = new TestModel(timestamp: 1234, message: 'test')
view = new TestView(model: model)
```

## 出力結果

```html
<div>
    <h3 class="timestamp">1234</h3>
    <p class="message">test</p>
</div>
```
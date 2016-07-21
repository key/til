# 3Dスキャナワークショップ

2016/06/08

DMM.make AKIBAのワークショップ

## 製品

### Artec 3D

ハンディタイプスキャナ。
プロジェクタで格子を投影してステレオカメラで認識。


### Rexscan III

固定式スキャナ。
スキャン対象のオブジェクトをベッドの上に置いて、
プロジェクタで講師を投影してステレオカメラで認識（Artec 3Dと同じ）。

焦点合わせはマニュアル。


## スキャンのコツ

### Artec 3D

スキャン時にオブジェクトを認識する距離を設定する。
床など必要のない対象物が写らないようにする。

可視光線を使ってスキャンしているため、黒いものや透明なものはスキャンしづらい。
なので、マットホワイト、マットグレーなどでペイントしてからスキャンするのが良い。

ソフトウェア

- 複数のスキャン結果をマージできる
    - 自動合わせ
        - スキャン結果がきれいならいけるかも
        - 処理遅い
    - マーカ合わせ
        - 鼻の頂点、アゴ、目尻、耳など特徴のある場所を設定するとよい
- 穴だらけのメッシュになる
    - ソフトで自動で穴埋めできる
- エクスポート
    - stlほか

余談

- 野菜チェック
    - Senseだと野菜がわからない

### Rexscan III

ソフトウェアでステレオカメラの像がプレビュー出来るので、スキャン前に以下の対応をする。

- ステレオカメラの両方で対象が見えるように
- 露出設定（露出オーバーする部分がないように）

ソフトウェアで複数のオブジェクトをマージできる（スティッチング？）。
この辺りはArtec 3Dと同じ。


# 総括

使い方が分かってしまえば簡単。
説明にこなれていない、スキャナが壊れているなど、講義内容としてはレベルが低い。
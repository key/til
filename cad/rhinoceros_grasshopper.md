# Rhinoceros Grasshopper

2016/03/02

[【DMM.make AKIBA ワークショップ】削り出しでつくる真鍮アクセサリー](http://peatix.com/event/151696)に参加。
特にアクセサリが欲しいわけではなかったんですが、Grasshopperを学びたかったので。GrasshopperはRhinocerosのプラグイン。

「コンポーネント」という単位で処理を接続していくことで、
3Dオブジェクトを生成することができる。
例えば式を元にサインカーブを3Dモデルに反映するとか、
スライダーをぐりぐりすると3角形から8角形までのポリゴンを作るといったことができる。


## 下準備

Mac版はRhinoceros WIPじゃないとだめ。評価版を90日間使うことができる。
Grasshopperの起動は、コマンドに`ExplicitHistory`とタイプする。

ちなみにタッチパッドだと操作が苦しいのでマウスがあった方が便利。

## 操作

- パン
    - Shift + 右ドラッグ
- Grasshopperでのコマンド起動
    - 任意の場所をダブルクリックするとコマンドを入力できる
- オブジェクトの選択
    - 左から選択する
        - 矩形に含まれたものが選択される
    - 右から選択する
        - 矩形が触れているものが選択される
- グループ化
    - CTRL+G
- rhinoからgrasshopperに持って行くには
    - rhinoでポイントを入れる
    - grasshopperでPointコンポーネント作る
        - set one pointでrhinoのポイントを選択する
      
## grasshopperで作るオブジェクト

- コンポーネント
    - 左が入力
        - コンポーネント毎に入力できる値が異なる
    - 右が出力
        - コンポーネントの出力が行われる
        - 複数のコンポーネントに同時に出力できる

## コンポーネント

- polygon
    - ポリゴンを出力する
    - 入力
        - セグメント数
        - 角丸
    - 出力
        - P Polygon
        - L Length
- number slider
    - 数字を出力するコンポーネント
    - コマンドラインで数字を入力しても良い
    - RNEOの値でスライダの動作を制御することが出来る
        - R Real number
        - N Neutral number
    - 上限、下限を設けておくと良い
        - エラーが下流にでんぱすると処理が遅くなる
- Rotate
    - オブジェクトを回転させる
    - 入力
        - G Geometry
        - A Angle
        - P Plane
    - 出力
        - G Geometry
- Radian
    - 角度をラジアンに変換するコンポーネント
    - 入力
        - D Degrees
    - 出力
        - R Radius
- Scale NU
    - ジオメトリをスケール（縮ませたり伸ばしたり）するコンポーネント
    - NU? 
    - 入力
        - X X軸？
        - Y Y軸？
    - 出力
        - ジオメトリ
- Golden
    - 黄金比に変換するコンポーネント。こんなのあるのかよ！
    - 入力
        - 数値
    - 出力
        - 入力を黄金比した値
- Extrude
    - オブジェクトをベクトル方向に押出す
    - Grasshopperは押し出しても天井地面を埋めてくれない
    - 入力
        - B Base（ジオメトリ）
        - D Direction (ベクトル)
    - 出力
        - ジオメトリ
- Populate 2D
    - ランダムにポイントを配置する
    - 入力
        - N Number
        - S Seed
    - 出力
        - ポイントのリスト
- Decontrust
    - リストからXYZを取り出す？
    - 入力
        - リスト？Populate 2Dのリストを受け取って、XYZを取り出す
    - 出力
        - X
        - Y
        - Z
- Random
    - ランダム値を出力するコンポーネント
- Construct Domain
    - AからBまでの値を作る
    - 入力
        - A
        - B
    - 出力
        - I Numeric domain
- Delaunay Mesh
    - ソリッドからメッシュを作る
    - 入力
        - ソリッド
    - 出力
        - メッシュ
- Flatten Tree
    - （わすれた）
- Cap
    - シリンダーやExtrudeで作ったオブジェクトの天井と地面を作る
    - 入力
        - ジオメトリ
    - 出力
        - ジオメトリ


## コツ

- ソリッドとメッシュがある。メッシュ＝Brep geometry
- 描画したいものだけプレビューすると軽い
    - sphereは重いのでコネクタを切る
- 値の手動変更
    - 部品を右クリックしてset number



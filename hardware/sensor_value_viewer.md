# センサ値のビュワー

2016/02/18

センサ値はビュワーが無いと不具合やエラーが把握しづらい。

ウェブアプリでもネイティブアプリでも、何でも良いのでビュワーが必要。
Excelなどでチャートを使うのも良いかもしれない。

大量のデータ、特殊なデータを扱うのであれば、データ量や速度の観点からネイティブアプリが良さそう。

- 6軸センサ
    - 大量のデータを出力することができる
        - 1kHzで記録すると1時間で360万サンプル
        - ウェブブラウザで扱うのはキツイ
    - 姿勢データ
        - オイラー角 / クォータニオン
        - センサ値を見ても分からない
        - 3Dモデルをぐるぐる回したほうが見やすい
- GPS
    - 緯度経度
        - 地図がないと意味不明

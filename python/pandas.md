# Pandas

2016/03/02

その昔pydata tokyoで教えてもらった内容を読み返しながら復習。

jupyter notebookで試した内容を順にまとめ。

```
# matplotlibをインライン表示
%matplotlib inline

import numpy as np
import pandas as pd

# データの集計ユーティリティ
from pandas.stats.moments import rolling_mean
```

pandasはCSVを直接読み込める。
読み込み後は`DataFrame` オブジェクトが返る。

```
# CSV読み込み
df = pd.read_csv('test.csv')

# CSVデータの概要を表示する（平均値、最大値、最小値などなど）
df.describe()
```

`head()`により先頭から任意のサンプルを表示できる。
スライスでアクセスしても同じ。

```
print df.head(10)
print df[:10]
```

`plot()`メソッドでmatplotlibを使って描画することが出来る。オプションによりいろいろ変更可能。

```
# そのまま描画
df.plot()

# 幅、高さを指定
df.plot(figsize=(16, 6))

# データの一部を描画
df[100:200].plot()

# 移動平均を描画
rolling_mean(df[100:200], 50).plot()
```

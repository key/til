# Autobahn Subscribe

2016/04/09

特定のルールでトピックをサブスクライブする。

以下のいずれかのルールでサブスクライブ出来る。

- 完全一致
- 前方一致
- 部分一致

## 完全一致

`subscribe()`のオプションを何もつけないと完全一致でマッチする。

以下は `com.example` にだけマッチする。

```coffee
session.subscribe('com.example', @onEvent)
```

## 前方一致

`subscribe()`にオプションをつけて前方一致にする。

以下は`com.example.notifications`などにマッチする。

```coffee
session.subscribe('com.example', @onEvent, {match: 'prefix'})
```

## 部分一致

別のオプションで部分一致もできる。

以下は`com.example.notifications.(なにか).update`にマッチする。

```coffee
session.subscribe('com.example..update', @onEvent, {match: 'wildcard'})
```

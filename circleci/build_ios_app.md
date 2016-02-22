# CircleCIでiOSアプリをビルドする話

2016/02/22

[ここらへん](https://circleci.com/docs/ios)のまとめ。

- CircleCIのiOSサポート状況はβ版
- Xcodeは以下をサポート
    - 7.0
    - 7.1.1
    - 7.2.1
    - 7.3 (beta)
- xctool
    - 0.2.8
- CocoaPods
    - 0.39.0

こんな感じの `circle.yml` を書く。

```
machine:
  timezone:
    Asia/Tokyo
  xcode:
    version: 7.2

dependencies:
  pre:
    - scripts/dependencies/pre.sh

test:
  override:
    - scripts/test.sh
```

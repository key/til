# WAMP

2016/03/25

WAMP=Web Application Messaging Protocolというオープンスタンダード（[公式サイト](http://wamp-proto.org/)）。

WebSocketを利用したRPCとPub/Subを提供するためのスタンダード、というかんじ。
現在プロトコルバージョン2が提供されている。

サーバサイド、クライアントサイド、モバイルアプリ、エンベデッドデバイスなど各種ライブラリが
存在しているので使いやすそう。Pythonでは[Autobahn | Python](http://autobahn.ws/python/)というライブラリがある。

具体的な用途としては、

- チャットアプリケーション
- センサモニタリングと監視画面（管理画面）
- RPCによる任意のコマンド実行

などが挙げられる。

WebAPIフレームワークではRESTfulアーキテクチャが多く採用されており、RESTfulなAPIエンドポイントを
通じてサーバサイドのモデルを操作するスタイルが一般的だが個人的に以下の問題があると感じていた。

- サーバのモデルスキーマ変更を行なった場合、容易にRESTful APIのパラメタを変更できない（破壊的な変更になる）
- サーバにジョブを投入するなど、モデル操作を行わない指令を行うことができない

前者はRESTful APIのエンドポイントの操作に対してモデル操作のマッピングを随時書く必要があるし、後者はRPCのような別の仕組みで対応する必要がある。

モデル操作をRPCで実施することにしてしまえば、

## 参考

- [WAMP](http://wamp-proto.org/)
- [Autobahn](http://autobahn.ws/)
- [Crossbar.io](http://crossbar.io)

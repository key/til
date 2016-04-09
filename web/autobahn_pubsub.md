# Autobahn Pub/Sub

2016/03/26

アウトバーンって読むのか？

Crossbar.ioと組み合わせてAutobahnのPython, JavaScript用のライブラリを試してみた。
といってもサンプルコードを写経しただけですが。


## Pub/Sub


`com.myapp.oncounter`というトピックを通じてメッセージを送受信するサンプル。

Pub/Sub自体はCrossbarが担当する。


### Crossbar.io

`/ws` にWebSocketのエンドポイントを置く。realmとroleはてきとうに。

```
{
  "version": 2,
  "controller": {},
  "workers": [
    {
      "type": "router",
      "options": {
        "pythonpath": [
          ".."
        ]
      },
      "realms": [
        {
          "name": "realm1",
          "roles": [
            {
              "name": "anonymous",
              "permissions": [
                {
                  "uri": "",
                  "match": "prefix",
                  "allow": {
                    "call": true,
                    "register": true,
                    "publish": true,
                    "subscribe": true
                  },
                  "disclose": {
                    "caller": false,
                    "publisher": false
                  },
                  "cache": true
                }
              ]
            }
          ]
        }
      ],
      "transports": [
            "ws": {
              "type": "websocket",
              "debug": true
            }
          }
        }
      ]
    }
  ]
}
```


### Python

`127.0.0.1:8000`に接続する。

`com.myapp.oncounter` トピックを通じてカウンタの値をPublish(送信)する。
カウンタは1秒に1ずつインクリメント。

```
from autobahn.twisted.wamp import ApplicationSession
from autobahn.twisted.wamp import ApplicationRunner
from autobahn.twisted.util import sleep
from twisted.internet.defer import inlineCallbacks


class MyComponent(ApplicationSession):
    @inlineCallbacks
    def onJoin(self, details):
        # 接続時に呼ばれるコールバック
        print("session ready")

        # 1秒毎にカウンタをインクリメントして `com.myapp.oncounter` に送信する
        counter = 0
        while True:
            self.publish(u'com.myapp.oncounter', counter)
            counter += 1
            yield sleep(1)


if __name__ == '__main__':
    runner = ApplicationRunner(url=u"ws://127.0.0.1:8000/ws", realm=u"realm1")
    runner.run(MyComponent)
```


### JavaScript

`127.0.0.1:8000`に接続する。

`com.myapp.oncounter` トピックをSubscribe(購読)してカウンタの値を受信する。
受信した値はJavaScript Consoleに出力。

```
# エンドポイントの設定
@connection = new autobahn.Connection(url: 'ws://127.0.0.1:8000/ws', realm: 'realm1')

# 接続時コールバックの設定
@connection.onopen = (session) =>
  # `com.myapp.oncounter` を購読して、値が飛んできたらコールバックを実行する
  session.subscribe('com.myapp.oncounter', (args) ->
    console.log("Event:", args[0])
  )

# 接続
@connection.open()
```


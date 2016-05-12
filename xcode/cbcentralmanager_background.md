# CBCentralManagerがバックグラウンドで通知を受け取れない

2016/05/12

アプリを起動して通知を購読し、ホームボタンを押して
バックグラウンドに移行させると通知を受け取れなった。次のように書いていた。

```objectivec
class AppDelegate: UIResponder, UIApplicationDelegate {

    var window: UIWindow?

    var manager: CBCentralManagerWrapper = CBCentralManagerWrapper.sharedInstance
    
    ...
}
```

```objectivec
class CBCentralManagerWrapper {
    public static let sharedInstance = CBCentralManagerWrapper()
    var manager: CBCentralManager? = nil
    
    private override init() {
        super.init()
        
        self.manager = CBCentralManager(delegate: self, queue: nil, options: nil)
    }
}
```

いろいろ調べた結果、 `AppDelegate.didFinishLaunchingWithOptions` の中に初期化処理を書く必要があった。

```objectivec
class AppDelegate: UIResponder, UIApplicationDelegate {

    var window: UIWindow?
    var manager: CBCentralManagerWrapper? = nil

    func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject:AnyObject]?) -> Bool {
        self.manager = CBCentralManagerWrapper.sharedInstance
        return true
    }
}
```

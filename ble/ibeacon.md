# iBeacon

2016/05/25

Appleのビーコン仕様。
iPhoneだとCoreLocationを使用してビーコンを認識、アプリケーションロジックを実行することが出来る。
ユースケースとしては、屋内位置測位や着席・離席みたいなのを認識するのに使える（と思う）。


## iBeaconパケットの構造

Stackoverflowのポストによれば、Bluetoothアドバタイズメント内にiBeacon用のデータを含めて送信するだけ。
iOSは`Company identifier code (0x004c)`および`Data type (0x02, 0x15)`でiBeaconパケットとして認識してビーコン識別に利用しているっぽい。

ユーザ（ビーコンの開発者）が指定できるのは以下の3つ、合計21バイト。

- UUID 16bytes
- Major 2bytes
- Minor 2bytes
- Tx Power 1byte


## iOSにおける開発
### iBeaconの発信

`CLBeaconRegion`クラスを使用して生成する。
UUID, major, minorを指定するには下記のイニシャライザが使える。

```objectivec
- (instancetype)initWithProximityUUID:(NSUUID *)proximityUUID
                                major:(CLBeaconMajorValue)major
                                minor:(CLBeaconMinorValue)minor
                           identifier:(NSString *)identifier
```

UUID文字列の生成にはコマンドラインで `uuid`コマンドを使う。

```objectivec
// UUIDを作る
NSUUID *uuid = [[NSUUID alloc] initWithUUIDString:@"E5C6390E-628A-481B-896F-F567E69E8574"];

// ビーコン生成
CLBeaconRegion *beaconRegion = [[CLBeaconRegion alloc] initWithProximityUUID: uuid,
                                                                       major: 1,
                                                                       minor: 1,
                                                                  identifier: @"org.mitsukuni.myRegion"];

// アドバタイズメントデータの生成
NSDictionary *peripheralData = [beaconRegion peripheralDataWithMeasuredPower: nil];

// アドバタイズ開始
CBPeripheralManager *peripheralManager = [[CBPeripheralManager alloc] initWithDelegate:self
                                                                                 queue:nil
                                                                               options:nil];
[peripheralManager startAdvertising:self.beaconPeripheralData];
```

### iBeaconの受信

iBeaconの受信はCoreLocationを使用する。

```objectivec
// UUID生成　ビーコンのUUIDと合わせること
NSUUID *uuid = [[NSUUID alloc] initWithUUIDString:@"E5C6390E-628A-481B-896F-F567E69E8574"];
CLBeaconRegion *beaconRegion = [[CLBeaconRegion alloc] initWithProximityUUID:uuid identifier:@"org.mitsukuni.myRegion"];

// ロケーションマネージャの初期化
CLLocationManager *locationManager = [[CLLocationManager alloc] init];
locationManager.delegate = self;
[locationManager startMonitoringForRegion:self.beaconRegion];
```

`CLLocationManager`のdelegateで`didEnterRegion`および`didExitRegion`が呼ばれる。

```objectivec
- (void)locationManager:(CLLocationManager *)manager didEnterRegion:(CLRegion *)region {
    [self.locationManager startRangingBeaconsInRegion:self.beaconRegion];
}

-(void)locationManager:(CLLocationManager *)manager didExitRegion:(CLRegion *)region {
    [self.locationManager stopRangingBeaconsInRegion:self.beaconRegion];
}
```

## 参考

- 公式
    - [iBeacon for Developers](https://developer.apple.com/ibeacon/)
    - [Getting started with iBeacon (PDF)](https://developer.apple.com/ibeacon/Getting-Started-with-iBeacon.pdf)

- [What is the iBeacon Bluetooth Profile](http://stackoverflow.com/questions/18906988/what-is-the-ibeacon-bluetooth-profile)

# Black Belt Online Seminar AWSサーバレスアーキテクチャ入門

2016/08/09

ウェビナーを聴講した。hashtag, #awsblackbelt

https://connect.awswebcasts.com/serverless-on-aws/?launcher=false

## アーキテクチャについて

サーバレスアーキテクチャと対比するため、既存のアーキテクチャを紹介していた。

### Monolithicアーキテクチャ

旧来の形。一つのユニットをチームで管理する。
問題が起きるとユニット全体でロールバックする必要がある。
システムの更新が大変になる。

### The Service Oriented Architecture (=SOA)

サービス思考のアーキテクチャ。

マルチティア型のアーキテクチャ。
ユニットをプレゼンテーション層、ロジック層などなどのモジュールに分離する。
個々のユニットインフラが分離していることが重要。

モジュールが分離しているため、スペシャライズされたメンバで構成できる。

### Microservicesアーキテクチャ

モジュールをブレイクダウンして細かなサービスに分割する。
マイクロサービス単位で開発、検証、配備。

### どのアーキテクチャが良いのか？

開発フェイズや組織によってどのアーキテクチャが最適か変わる。

### 既存のアーキテクチャの良いところ、悪いところ

- pros
    - 支援ツールが多い
    - AWS上でもEC2やELBなど多くのツールを提供している。
- cons
    - 相互に依存しあっている
    - →そこでサーバレスアーキテクチャ！

### サーバレスアーキテクチャのいいところ

- 運用不要
- スケーラブル
- ビジネスロジックだけ書けば良い

## サーバレスアーキテクチャ

主にAWSサービスを利用した内容。

- Lambda = マイクロサービスの個々のモジュールに相当

Lambdaのコンポーネント

- lambda function
    - ユーザのカスタムコード(python, nodejs, java, scalar, jruby)
    - メモリとかCPUとかIAMのロールなどのリソース含まれる
        - **IAMが入ってるのでコードに認証情報を含める必要がない**
    - **実行時間は最大5分**        
    - CPU性能とメモリ量は正比例、ネットワーク帯域や速度にも影響する
        - 最小128MB
        - 最大1.5GB
- event source
    - いわゆるトリガー
    - AWSサービスをイベントソースに出来る
        - S3, kinesis, SNS, dynamo, cloudwatchなどなど
    - イベントをlambdaハンドラに渡す
    - 例: S3への保存をトリガに、アップロードされたファイルを処理
- lambda service
    - 関数を実行する機能のAPIもある（イベント以外でも実行できる）
- function network environment
    - Default or Customer VPC
    - Default
        - プライベートVPCにはアクセスできない
            - S3は操作できるけど、RDSは操作できないなど
    - Customer VPC
        - 注意点
            - public interfaceにはアクセスできない=インターネットアクセスできない
            - KinesisのようにVPCを持たないサービスにアクセスするには、NATを利用する必要がある

## API Gateway

- ブラウザ上でRESTful APIを作成する感じ
- リクエストに対してバックエンドの処理を実行する=lambdaの処理を実行する
- JSONオブジェクトをマッピングしてDynamoDBに保存することが容易に出来る
    - マッピングだけ変えれば裏側のスキーマは自由に変更できる
- APIを作る、テストする、ステージを選んでデプロイ
    - ステージを選ぶことが出来る
− エクスポート
    - swaggerなど

## 実例
### PlayOn! Sports

Re:Inventで発表された。リンクのURLから見られる（開けない…）。

- カメラで撮影されたデータをノートPCからS3にアップロードする
    - HLSでチャンクを生成してアップロード
    − CloudFrontで受け取ってS3保存
    - Lambda関数でカスケードして変換
        - HQコピー
        - 480pトランスコード
        - 360pトランスコード
        - 音声のみ
        - thumbnail
    - S3に保存して、CloudFrontで再配信 

## そのほか

- 独自認証はLambda Custom authorizerを使える

## サーバレスアーキテクチャパターン

- microservice
    - lambdaのみで実現できることが多い
- モバイルバックエンド
    - API Gateway -> lambda -> SNS等
- リアルタイム分析
    - Kinesis -> Lambda -> Dynamo等

## サーバレスベストプラクティス

lambda

- ファンクションサイズを制限する
    - 初回実行時に時間がかかる
    - 特にJVMは起動が遅い
- Lambda実行コンテナの再利用を期待しない
- ディスクサイズ500MB使える。キャッシュなどにどうぞ
- 付属のロガーを使う
- カスタムメトリクスを使う 

API Gateway

- mock integrationを活用する（仮API）
    - 実装がなくても開発ができる
- エンドユーザアクセス制御はCognitoを組み合わせる
- マッピングテンプレートを利用して、フロントとバックエンドのインターフェースを統一する

そのほか

- 使いまわしできない名前を使う
- 命名規則とバージョンイングを使用する
− 権限を最小化する、IAMロールに適切な権限を与える
    - **lambdaとIAMロール 1:1がよい**
- 大規模なスケーリングイベントがあるようであれば、AWSサポートに連絡するのが良い

## 資料

- [Getting started with serverless architectures](http://www.slideshare.net/AmazonWebServices/getting-started-with-serverless-architectures-63429092)

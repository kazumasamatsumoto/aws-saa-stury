# Kinesis

Amazon Kinesisは、ストリーミングデータをリアルタイムで収集、処理、分析するためのフルマネージドサービスです。大規模なデータストリームを簡単に扱うことができます。

# Kinesis Data Streams

リアルタイムでデータストリームを収集・処理するためのサービスです。

## 主な特徴

- **スケーラビリティ**
  - シャードベースのアーキテクチャ
  - 無制限のスループット拡張が可能
  - 各シャードは1MB/秒の書き込み、2MB/秒の読み取り容量

- **データ保持**
  - デフォルトで24時間
  - 最大365日まで延長可能
  - 保持期間中は何度でもデータを再処理可能

- **耐久性**
  - 3つのアベイラビリティーゾーンに同期レプリケーション
  - データの耐久性と可用性を確保

## ユースケース

- リアルタイムメトリクスとレポート
- リアルタイムデータ分析
- 複雑なストリーム処理
- モバイルデータキャプチャ

# Kinesis Data Firehose

ストリーミングデータを各種デスティネーションに配信するためのフルマネージドサービスです。

## 主な特徴

- **自動スケーリング**
  - インフラストラクチャ管理不要
  - データ量に応じて自動的にスケール

- **データ変換**
  - Lambda関数を使用したデータ変換
  - フォーマット変換（JSON、Parquet等）
  - データの圧縮

- **バッチ処理**
  - データのバッファリング
  - 効率的なデータ配信

## サポートされるデスティネーション

- Amazon S3
- Amazon Redshift
- Amazon OpenSearch Service
- Splunk
- HTTP Endpoint
- サードパーティサービス

# Kinesis Data Analytics(Apache Flink)

SQLまたはApache Flinkを使用してストリーミングデータをリアルタイムで分析するサービスです。

## 主な特徴

- **SQLクエリ**
  - 標準SQLを使用したストリーム分析
  - 時系列分析
  - 複雑なイベント処理

- **Apache Flink**
  - オープンソースの分散処理フレームワーク
  - 高度なストリーム処理機能
  - カスタムアプリケーション開発

## ユースケース

- リアルタイムメトリクス計算
- 時系列分析
- 異常検知
- イベント相関分析

# Kinesis Video Streams

ビデオストリームをキャプチャ、処理、保存するためのフルマネージドサービスです。

## 主な特徴

- **ストリーミング機能**
  - リアルタイムビデオストリーミング
  - 双方向通信サポート
  - WebRTC対応

- **統合機能**
  - 機械学習サービスとの連携
  - リアルタイム分析
  - ビデオ処理パイプライン

## ユースケース

- ビデオ監視システム
- スマートホームカメラ
- 産業用モニタリング
- ビデオ会議アプリケーション

## Elastic Transcoder

メディアファイルを様々なフォーマットに変換するためのサービスです。

- **主な機能**
  - 動画フォーマット変換
  - 解像度調整
  - サムネイル生成
  - DRM対応

# Amazon Managed Streaming for Apache Kafka(MSK)

フルマネージドのApache Kafkaサービスです。

## 主な特徴

- **管理の簡素化**
  - クラスター管理の自動化
  - パッチ適用の自動化
  - モニタリング統合

- **セキュリティ機能**
  - 暗号化（保管時および転送時）
  - IAM認証
  - VPCネットワーキング

- **高可用性**
  - マルチAZ配置
  - 自動フェイルオーバー
  - データレプリケーション

## Apache Kafka

分散ストリーミングプラットフォームです。

### 主な特徴

- **高スループット**
  - 大量のメッセージ処理
  - 低レイテンシー配信

- **スケーラビリティ**
  - 水平スケーリング
  - パーティション分散

- **耐久性**
  - メッセージの永続化
  - レプリケーション
  - フォールトトレランス

### ユースケース

- イベントソーシング
- ログ集約
- ストリーム処理
- メッセージングシステム

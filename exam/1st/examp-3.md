# VPC 内の EC2 から S3 への安全なアクセス方法

## 問題のポイント

- アジア企業が S3 に顧客データを保存
- EC2 インスタンスは VPC 内で実行
- インターネット経由のアクセスを制限したい
- アクセスを最小限に抑えたい

## 正解

A. VPC 内で Amazon S3 用の VPC ゲートウェイエンドポイントを設定
C. アプリケーションが実行されている VPC 内のインスタンスのみにアクセスを許可する S3 バケットポリシーを設定

## 解説

### なぜ A と C が正解なのか

1. VPC ゲートウェイエンドポイント（A）

   - インターネットを経由せずに VPC 内から S3 にアクセス可能
   - プライベートな接続を確保
   - データ転送のセキュリティを強化

2. S3 バケットポリシー（C）
   - 特定の VPC 内のインスタンスのみにアクセスを制限
   - 最小権限の原則に従う
   - きめ細かなアクセス制御が可能

### 他の選択肢が不正解な理由

B. S3 バケットを公開する

- セキュリティリスクが高い
- 要件の「アクセスを制限」に反する

D. IAM 認証情報を直接 EC2 にコピー

- セキュリティのベストプラクティスに反する
- 認証情報の漏洩リスク
- 代わりに IAM ロールを使用すべき

E. NAT ゲートウェイの使用

- S3 アクセスには不要
- コスト増加
- セキュリティ要件を満たさない

## 実装のベストプラクティス

1. VPC エンドポイントの設定
2. 適切な IAM ロールの作成
3. 最小権限を持つバケットポリシーの設定
4. エンドポイントポリシーによる追加のアクセス制御

## 参考資料

- [VPC エンドポイントガイド](https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints.html)
- [S3 のセキュリティベストプラクティス](https://docs.aws.amazon.com/AmazonS3/latest/userguide/security-best-practices.html)

# S3 へのファイルアップロード後の自動処理アーキテクチャ

## 問題のポイント

- 小さなファイルを S3 にアップロード
- データを変換してキーバリュー形式で保存
- できるだけ早い処理が必要
- 需要が変動する（アップロード数の増減が大きい）
- 運用負担を最小限にしたい

## 正解

C. S3 → SQS → Lambda → DynamoDB の構成

## 解説

### なぜ C が正解なのか

1. サーバーレスアーキテクチャの利点

   - インフラ管理が不要
   - 自動スケーリング
   - 従量課金制
   - 運用負担が最小限

2. 各コンポーネントの役割
   - S3：ファイルのアップロード先
   - SQS：イベントの一時保管とバッファリング
   - Lambda：データ処理と変換
   - DynamoDB：キーバリュー形式でのデータ保存

### 他の選択肢が不正解な理由

A. Amazon EMR + Aurora

- 小規模処理には過剰
- 常時稼働が必要で非効率
- 運用負担が大きい

B. EC2 + SQS + DynamoDB

- EC2 の管理が必要
- スケーリングの設定が複雑
- 運用コストが高い

D. EventBridge + Kinesis + Lambda + Aurora

- アーキテクチャが複雑すぎる
- ストリーミング処理は不要
- コスト効率が悪い

## 実装のポイント

1. S3 イベント通知の適切な設定
2. SQS のメッセージ保持期間の設定
3. Lambda のタイムアウト設定
4. DynamoDB のキャパシティ設定

## 参考資料

- [Lambda with SQS](https://docs.aws.amazon.com/lambda/latest/dg/with-sqs.html)
- [S3 イベント通知](https://docs.aws.amazon.com/AmazonS3/latest/userguide/EventNotifications.html)

# RDS MySQL のリードレプリカによるパフォーマンス改善

## 問題の違いと特徴

### 前回の問題（Aurora クローン）

- **目的**: 開発環境の作成
- **課題**: 4 時間ごとのエクスポートによる本番環境への影響
- **要件**: 開発チームの作業効率向上
- **解決策**: Aurora のクローン機能（独立した環境を即時作成）

### 今回の問題（RDS リードレプリカ）

- **目的**: 本番環境のパフォーマンス向上
- **課題**: 読み取りリクエスト集中時の処理遅延
- **要件**: 読み書きトラフィックの分離
- **解決策**: リードレプリカの追加（読み取り負荷の分散）

## 正解

D. データベースにリードレプリカを作成し、元のデータベースと同じリソースを使用

## 解説

### なぜ D が正解なのか

1. リードレプリカの特徴

   - 読み取り専用の複製を作成
   - メイン DB の負荷を軽減
   - 同期的にデータを複製
   - スケーラブルな読み取り性能

2. 同じリソースサイズが必要な理由
   - 同等の処理能力が必要
   - 負荷分散の効果を最大化
   - パフォーマンスの一貫性を確保

### 他の選択肢が不正解な理由

A. Multi-AZ 構成

- 可用性向上が目的
- 読み取り負荷分散には非対応
- パフォーマンス改善に直接効果なし

B. セカンダリからの読み取り

- Multi-AZ のセカンダリは待機用
- 読み取りリクエストを処理不可
- アーキテクチャとして不適切

C. 小さいリソースのリードレプリカ

- 処理能力不足のリスク
- パフォーマンス低下の可能性
- コスト削減より性能優先すべき

## 実装のポイント

1. リードレプリカの適切なサイジング
2. アプリケーションでの読み取り振り分け設定
3. レプリケーション遅延のモニタリング
4. フェイルオーバー戦略の検討

## 参考資料

- [RDS リードレプリカ](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ReadRepl.html)
- [RDS のベストプラクティス](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_BestPractices.html)

# 高性能ファイルシステム FSx for Lustre の活用

## 問題のポイント

- オンプレミスの 3D レンダリングアプリケーション
- Lustre クライアントを使用
- 高速データアクセスが必要
- 完全管理型のストレージソリューションが必要

## Lustre とは

1. 基本概念

   - **名称の由来**: Linux + Cluster = Lustre
   - **特徴**: 高性能な分散ファイルシステム
   - **用途**: スーパーコンピューターや大規模クラスター向け

2. 主な特徴
   - 並列データアクセス
   - 高スループット
   - 大規模なデータセット処理
   - HPC（High Performance Computing）に最適

## 正解

D. Amazon FSx for Lustre ファイルシステムを作成

### なぜ D が正解なのか

1. FSx for Lustre の利点

   - フルマネージド型サービス
   - Lustre プロトコルのネイティブサポート
   - 高性能なデータアクセス
   - オンプレミス環境との統合が容易

2. 要件との適合性
   - Lustre クライアントのサポート
   - 管理負担の軽減
   - 高速データアクセスの実現
   - スケーラブルな構成

### 他の選択肢が不正解な理由

A. Storage Gateway

- Lustre プロトコル非対応
- パフォーマンスが要件を満たさない
- 用途が異なる（ハイブリッドストレージ）

B. EC2 + NFS

- 管理が必要（非マネージド）
- Lustre プロトコル非対応
- 構築・運用の負担大

C. Amazon EFS

- Lustre プロトコル非対応
- HPC 向けの最適化がない
- 3D レンダリング用途には不適切

## 実装のポイント

1. FSx for Lustre の適切なサイジング
2. ネットワーク構成の最適化
3. セキュリティグループの設定
4. バックアップ戦略の検討

## 参考資料

- [FSx for Lustre の概要](https://docs.aws.amazon.com/fsx/latest/LustreGuide/what-is.html)
- [Lustre ファイルシステムについて](https://www.lustre.org/about/)

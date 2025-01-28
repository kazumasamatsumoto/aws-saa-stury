# AWS Transfer Family

AWS Transfer Family は、SFTP（SSH File Transfer Protocol）、FTPS（File Transfer Protocol over SSL）、FTP（File Transfer Protocol）プロトコルを使用して、Amazon S3 バケットや Amazon EFS ファイルシステムとの間でファイル転送を行うことができるフルマネージドサービスです。

## 主な特徴

### サポートされるプロトコル
- **SFTP**: SSH File Transfer Protocol
- **FTPS**: File Transfer Protocol over SSL/TLS
- **FTP**: File Transfer Protocol（非推奨 - セキュリティ上の理由から）

### ストレージ統合
- **Amazon S3**: オブジェクトストレージとの統合
- **Amazon EFS**: ファイルシステムとの統合

### エンドポイントタイプ
- **パブリックエンドポイント**: インターネット経由でアクセス可能
- **VPCエンドポイント**: VPC内からのみアクセス可能
  - プライベートサブネット内のリソースからのアクセス
  - セキュリティグループによるアクセス制御

### 認証方式

#### IAMロールベース認証
- IAMロールを使用してアクセス権限を管理
- きめ細かなアクセス制御が可能
- AWS リソースへのアクセスを制御

#### セッションポリシー
- 一時的なアクセス権限の付与
- セッション単位でのアクセス制御
- より詳細な権限管理が可能

#### ID認証
- **AWS Directory Service for Microsoft Active Directory**
  - 既存のActive Directoryとの統合
  - Windows認証基盤の活用
- **API Gateway経由の独自認証**
  - カスタム認証システムの統合
  - 既存の認証基盤との連携

## ユースケース

- オンプレミスからクラウドへのデータ移行
- パートナーとのファイル共有
- バックアップソリューション
- データ収集パイプライン
- コンプライアンス要件のあるファイル転送

## セキュリティ機能

- 転送中のデータの暗号化（FTPS、SFTPの場合）
- 保管中のデータの暗号化（S3、EFSの暗号化機能）
- VPCエンドポイントによるネットワークレベルの分離
- IAMによる詳細なアクセス制御
- AWS CloudTrailによる監査ログの記録

## 利点

- フルマネージドサービス（インフラストラクチャの管理不要）
- 既存のファイル転送ワークフローとの互換性
- スケーラブルなアーキテクチャ
- 高可用性と耐久性
- セキュアなファイル転送
- 既存の認証システムとの統合

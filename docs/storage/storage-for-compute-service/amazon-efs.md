# Amazon Elastic File System (EFS)

Amazon EFS は、AWS クラウドサービスとオンプレミスリソースで使用できる、完全マネージド型の NFS ファイルシステムを提供するサービスです。

# NFS ファイルシステムとは

NFS ファイルシステム（Network File System）は、ネットワークを介してファイルを共有するための仕組みです。

## 身近な例えで理解する NFS

オフィスでの共有フォルダをイメージしてください：

- 複数の社員が同じ文書にアクセスできる「共有フォルダ」のようなものです
- 誰かがファイルを更新すると、他の人もすぐにその変更を見ることができます
- まるでローカルのフォルダのように使えますが、実際のデータは別のサーバーに保存されています

## NFS の主なメリット

1. **簡単な共有**

   - 複数のコンピュータから同じファイルにアクセス可能
   - ファイルのコピーを作る必要がない

2. **一元管理**

   - データを 1 か所で管理できる
   - バックアップも一括で行える

3. **リアルタイムな共同作業**
   - 複数のユーザーが同時に作業可能
   - 変更がリアルタイムで反映される

## 使用例

- 会社での文書共有
- 写真や動画の共有ストレージ
- サーバー間でのデータ共有
- バックアップストレージ

## 注意点

- インターネット接続が必要
- ネットワークの速度に依存
- 適切なアクセス権限の設定が重要

## 主な特徴

- **フルマネージドサービス**: インフラストラクチャの管理が不要で、自動的にスケーリングします。
- **高可用性と耐久性**: データは複数のアベイラビリティーゾーンに自動的にレプリケートされます。
- **NFSv4 プロトコル**: 標準的なファイルシステムインターフェースをサポートしています。
- **動的なスケーリング**: ストレージ容量は使用に応じて自動的に拡張・縮小します。

## ユースケース

- **コンテンツ管理とウェブサービス**: 大規模なコンテンツリポジトリの管理
- **ビッグデータ分析**: 分析アプリケーション用の共有ファイルシステム
- **メディア処理ワークフロー**: メディアファイルの処理と共有
- **コンテナストレージ**: ECS や EKS のための永続的ストレージ

## ストレージクラス

### 標準ストレージクラス

- 頻繁にアクセスされるデータに最適
- 高いパフォーマンスを提供
- より高いコスト

### EFS IA ストレージクラス（Infrequent Access）

- アクセス頻度の低いファイル向け
- 標準クラスと比べて低コスト
- データアクセス時に追加料金が発生

## セキュリティ機能

- **暗号化**: 保存データと転送中のデータの暗号化をサポート
- **IAM との統合**: きめ細かなアクセス制御が可能
- **VPC との統合**: ネットワークレベルでの分離を実現

## パフォーマンスモード

### 汎用パフォーマンスモード

- デフォルトのパフォーマンスモード
- ほとんどのユースケースに適している

### 最大 I/O パフォーマンスモード

- 高い同時実行性が必要な場合に最適
- より高いレイテンシーを許容する必要がある

## スループットモード

### バーストスループット

- デフォルトのスループットモード
- ファイルシステムのサイズに基づいてスループットが変動

### プロビジョンドスループット

- 一貫したパフォーマンスが必要な場合に使用
- 必要なスループットを事前に指定可能

## 料金体系

- ストレージ使用量に基づく課金
- スループットモードに応じた追加料金
- データ転送量に応じた料金
- IA ストレージクラスの場合のアクセス料金

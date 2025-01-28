# Amazon DocumentDB

## 概要

- MongoDB 3.6、4.0、5.0 と互換性のあるドキュメント指向型データベースサービス
- 既存の MongoDB アプリケーションから AWS へシームレスに移行可能
- Server Side Public License (SSPL)提供の MongoDB と互換性がある高パフォーマンスでスケーラブルなサービス

## 主なユースケース

- コンテンツ管理システム（CMS）
- リアルタイムアナリティクス
- モバイル、Web アプリケーション
- カタログ管理

## 特徴

### RDB と比較した特徴

- スキーマレスで柔軟なデータ構造
- 水平スケーリングが可能

### Key-Value 型データベースと比較した特徴

- リッチなデータ構造と複雑なクエリに対応
- 1 つのエンティティを 1 つのドキュメントとして表現し、関連データを一緒に格納

## システム構成

- DB インスタンス：0 ～ 16 個
  - プライマリインスタンス（読み書き可能）
  - レプリカインスタンス（読み取り専用）：最大 15 個
- クラスターボリューム
  - 3 つの AZ にわたって 6 個配置
  - 最大容量：128 TiB

### クラスターの構成要素

#### クラスターエンドポイント

- プライマリインスタンスへの接続に使用
- フェイルオーバー時に新しいプライマリインスタンスに自動的に接続

#### リーダーエンドポイント

- 読み取り専用のレプリカインスタンスへの接続に使用
- 読み取りワークロードを分散

#### インスタンスエンドポイント

- 特定のインスタンスへの直接接続に使用
- デバッグやメンテナンス作業時に利用

### セキュリティ機能

- AWS KMS による保存データの暗号化
- 転送中のデータの TLS 暗号化
- VPC 内でのセキュアな通信
- IAM によるアクセス制御
- セキュリティグループによるネットワークアクセス制御

### バックアップと復元

- 自動バックアップ
  - 最大 35 日間保持可能
  - 日次バックアップ
  - ポイントインタイム復元が可能
- 手動スナップショット
  - 任意のタイミングで取得可能
  - 無期限に保持可能

## クエリ例

### 1. データの挿入（Insert）

```javascript
db.books.insert({
  title: "The Great Gatsby",
  author: "F. Scott Fitzgerald",
  year: 1925,
  genres: ["Novel"],
  ratings: [
    { user: "user1", rating: 5 },
    { user: "user2", rating: 4 },
  ],
});
```

### 2. データの検索（Find）

```javascript
db.books.find({ author: "F. Scott Fitzgerald" });
```

### 3. データの更新（Update）

```javascript
db.books.update(
  { author: "F. Scott Fitzgerald" },
  { $set: { genres: ["Novel", "Fiction"] } }
);
```

### 4. データの削除（Remove）

```javascript
db.books.remove({ author: "F. Scott Fitzgerald" });
```

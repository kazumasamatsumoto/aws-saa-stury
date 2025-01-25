# AWS のタグ付け

タグ付けは、AWS リソースを効率的に管理・整理するための重要な機能です。

## タグとは

タグは、AWS リソースに割り当てるラベルで、キーと値のペアで構成されています。例：

- Key: Environment, Value: Production
- Key: Project, Value: ProjectA
- Key: Owner, Value: TeamB

## タグ付けのベストプラクティス

### 1. 命名規則の統一

- 一貫性のある命名規則を使用する
- 大文字小文字の使用を統一する
- スペースの代わりにハイフンまたはアンダースコアを使用する

### 2. 必須タグの定義

以下のような基本的なタグを設定することを推奨：

- Environment（環境）: prod, dev, staging など
- Project（プロジェクト名）
- Owner（所有者/担当チーム）
- CostCenter（コストセンター）
- Application（アプリケーション名）

### 3. コスト管理のためのタグ付け

- コスト配分タグを使用して、リソースごとの費用を追跡
- AWS Cost Explorer でタグベースのレポートを作成可能
- 部門やプロジェクトごとの費用を可視化

### 4. 自動タグ付け

- AWS Organizations のタグポリシーを使用
- CloudFormation テンプレートでタグを定義
- AWS Config ルールでタグの強制適用

## タグの制限事項

- リソースあたり最大 50 個のタグ
- キーは最大 128 文字（UTF-8）
- 値は最大 256 文字（UTF-8）
- キーと値は大文字小文字を区別
- タグキーの先頭に「aws:」は使用不可（AWS システム用に予約）

## タグ付けの管理ツール

- Tag Editor: 複数リソースのタグを一括編集
- Resource Groups: タグベースでリソースをグループ化
- AWS Config: タグポリシーの遵守状況を監視
- AWS Organizations: 組織全体でタグポリシーを管理

## セキュリティとアクセス制御

- IAM ポリシーでタグベースのアクセス制御が可能
- 特定のタグが付いたリソースのみにアクセスを制限
- タグの追加・変更権限を制御可能

## タグ付けの例

```json
{
  "Environment": "production",
  "Project": "e-commerce",
  "Owner": "team-shopping",
  "CostCenter": "cc-123456",
  "Application": "shopping-cart",
  "SecurityLevel": "high",
  "BackupPolicy": "daily"
}
```

## 関連サービス

- AWS Cost Explorer
- AWS Budgets
- AWS Resource Groups
- AWS Config
- AWS Organizations

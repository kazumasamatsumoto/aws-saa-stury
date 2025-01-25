# AWS Config

## 概要

- AWS リソースの構成変更を記録し、評価するためのサービス
- 設定変更の履歴管理とコンプライアンス評価を実施
- セキュリティとガバナンスの強化を支援

![AWS Config Overview](/image/management-monitoring&governance/logging-monitoring/config-overview.svg)

## Config ルール

設定可能なルールのタイプと評価方法：

![AWS Config Rules](/image/management-monitoring&governance/logging-monitoring/config-rules.svg)

### AWS Managed Rules

- AWS が提供する事前定義されたルール
- 一般的なセキュリティ要件やベストプラクティスに基づく
- 例：restricted-ssh（非準拠のセキュリティグループを検出）

### Customer Managed Rules

- ユーザーが定義するカスタムルール
- Lambda 関数を使用して独自の評価ロジックを実装
- 組織固有の要件に対応可能

### ルールの評価方法

1. **連続的評価**

   - リソースの変更時にリアルタイムで評価
   - 即時の非準拠検出が可能

2. **定期的評価**
   - 1 日 1 回の定期的な評価
   - バッチ処理による効率的な評価

## 自動修復機能

- 非準拠リソースの自動修復が可能
- Systems Manager の Automation 機能を使用
- 修復アクションの定義と実行

## 高度な機能

### クエリ機能

- 設定変更の履歴検索
- 特定条件での構成情報の抽出
- カスタムクエリの作成

### 拡張機能

- オンプレミスリソースの管理（AWS Systems Manager 経由）
- マルチアカウント対応
- マルチリージョン対応

## 料金体系

![AWS Config 料金体系](/image/management-monitoring&governance/logging-monitoring/config-pricing.svg)

課金の基準となる要素：

- Config ルールの数
- Conformance Packs の使用
- 設定スナップショットの S3 保存

## 問題解決シナリオ

![AWS Config 問題解決シナリオ](/image/management-monitoring&governance/logging-monitoring/config-scenario.svg)

## ベストプラクティス

1. **効率的な監視設定**

   - 必要なリソースタイプの選択
   - 適切なルール評価頻度の設定
   - 重要度に基づくルールの優先順位付け

2. **コスト最適化**

   - 必要なルールのみを有効化
   - 適切な評価頻度の選択
   - 不要なスナップショットの削除

3. **セキュリティ強化**
   - 重要な設定変更の監視
   - 自動修復の適切な設定
   - 定期的なコンプライアンス評価

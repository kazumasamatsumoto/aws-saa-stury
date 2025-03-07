# AWS CloudTrail

## 概要

- AWS アカウントのガバナンス、コンプライアンス、運用監査、リスク監査を行うためのサービス
- ユーザーアクティビティや API 操作を証跡（Trail）として記録
- アカウントのセキュリティと運用の最適化を支援

![CloudTrail Overview](/image/management-monitoring&governance/logging-monitoring/cloudtrail-overview.svg)

## イベントタイプ

CloudTrail で記録される 3 種類のイベント：

![CloudTrail Events](/image/management-monitoring&governance/logging-monitoring/cloudtrail-events.svg)

### 管理イベント

- AWS リソースの管理操作に関連するイベント
- 例：EC2 インスタンスの起動、IAM ポリシーの更新
- セキュリティとコンプライアンスの監査に重要

### データイベント

- リソースに対するデータ操作に関連するイベント
- 例：S3 バケット内のオブジェクトへの Put、Get、Delete 操作
- 高頻度で発生する可能性があり、選択的な記録が推奨

### CloudTrail Insights

- 通常のパターンから逸脱したアクティビティを検出
- API コール量とエラー率の異常を監視
- Write 管理 API と Read/Write 管理 API に対して生成

## セキュリティと保管

### 証跡の保管

- 過去 90 日分は無料で保管
- 長期保管は S3 バケットに保存
- 暗号化オプション：
  - SSE-S3（デフォルト）
  - AWS KMS カスタマーキー

### セキュリティ対策

1. 証跡の保護

   - KMS による暗号化
   - S3 バケットポリシーと IAM ポリシーの適用
   - MFA delete の設定

2. アクセス管理
   - 証跡保管用の専用アカウント作成
   - 運用担当者とセキュリティ管理者の分離
   - ダイジェストファイルによる改ざん検知

## ベストプラクティス

1. **監視設定**

   - 重要なイベントの選択的記録
   - 適切な保持期間の設定
   - 定期的なログ分析

2. **セキュリティ強化**

   - 暗号化の有効化
   - アクセス制御の徹底
   - 証跡の完全性確保

3. **コスト最適化**
   - 必要なイベントのみ記録
   - 適切な保存期間の設定
   - 定期的な使用状況の確認

# CloudWatch

1. **背景**:

- クラウド環境での監視の複雑さに対応するために生まれました
- 複数システムの統合監視という課題を解決しています
- カスタマイズ可能な監視基盤を提供しています

![CloudWatchが生まれた背景](/image/management-monitoring&governance/logging-monitoring/cloudwatch-background.svg)

2. **利用手順**:

- 段階的な導入が可能で、各ステップが明確です
- IAM ロールの設定から始まり、実際の監視設定まで順を追って進められます
- 設定のポイントを押さえることで、効果的な監視が実現できます

![CloudWatch利用手順](/image/management-monitoring&governance/logging-monitoring/cloudwatch-setup.svg)

3. **仕組み**:

- データ収集 → 処理・分析 → アクションの流れが明確です
- 各段階で必要な機能が統合されています
- 柔軟なカスタマイズと自動化が可能です

![CloudWatchの仕組み](/image/management-monitoring&governance/logging-monitoring/cloudwatch-architecture.svg)

4. **主要コンポーネント**:

## CloudWatch Metrics

- システムメトリクスの収集と分析
- カスタムメトリクスの作成が可能
- 統計情報の表示（平均、最大、最小、合計、パーセンタイル）

![CloudWatch Metrics](/image/management-monitoring&governance/logging-monitoring/cloudwatch-metrics.svg)

## CloudWatch Logs

- ログの一元管理とリアルタイム監視
- ログの保持期間設定（1 日～ 10 年、または無制限）
- ログパターンの検索とフィルタリング

![CloudWatch Logs](/image/management-monitoring&governance/logging-monitoring/cloudwatch-logs.svg)

## CloudWatch Alarms

- メトリクスに基づくアラート設定
- 複数条件の組み合わせが可能
- SNS 通知や Auto Scaling などのアクションと連携

![CloudWatch Alarms](/image/management-monitoring&governance/logging-monitoring/cloudwatch-alarms.svg)

## CloudWatch Events/EventBridge

- イベントベースの自動化
- スケジュール実行
- サービス間連携の orchestration

![CloudWatch Events](/image/management-monitoring&governance/logging-monitoring/cloudwatch-events.svg)

5. **ベストプラクティス**:

![CloudWatch ベストプラクティス](/image/management-monitoring&governance/logging-monitoring/cloudwatch-best-practices.svg)

## 監視設計

- 必要なメトリクスの特定
- アラートしきい値の適切な設定
- ログ収集戦略の策定

## コスト最適化

- 必要なメトリクスのみ収集
- 適切なログ保持期間の設定
- 不要なアラームの削除

## セキュリティ

- IAM ロールによる適切なアクセス制御
- 暗号化の有効化
- 監査ログの有効化

6. **SAA 試験のポイント**:

![CloudWatch SAA試験ポイント](/image/management-monitoring&governance/logging-monitoring/cloudwatch-saa-points.svg)

## 重要な概念

- メトリクス名前空間
- ディメンション
- 統計期間
- アラーム状態

## 統合サービス

- Auto Scaling
- SNS
- Lambda
- Systems Manager

## トラブルシューティング

- メトリクス収集の問題
- アラーム設定の問題
- ログ収集の問題

7. **料金体系**:

![CloudWatch 料金体系](/image/management-monitoring&governance/logging-monitoring/cloudwatch-pricing.svg)

- メトリクス収集・保存

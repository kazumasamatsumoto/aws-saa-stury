# AWS Savings Plans

AWS Savings Plans は、AWS の使用料金を大幅に削減できる柔軟な料金モデルです。1 年間または 3 年間の利用を約束することで、通常のオンデマンド料金と比較して最大 72%の割引を受けることができます。

## Savings Plans の種類

### 1. Compute Savings Plans

- EC2、Lambda、Fargate の使用に適用
- 最も柔軟な料金プラン
- インスタンスファミリー、サイズ、OS、テナンシー、リージョンに関係なく適用可能
- 最大 66%の割引

### 2. EC2 Instance Savings Plans

- 特定のインスタンスファミリーとリージョンに限定
- より高い割引率（最大 72%）
- インスタンスサイズ、OS、テナンシーは柔軟に変更可能

### 3. SageMaker Savings Plans

- Amazon SageMaker の使用に特化
- 最大 64%の割引
- すべての SageMaker インスタンスタイプに適用可能

## 主な特徴

- **柔軟性**: インスタンスタイプやリージョンを自由に変更可能
- **支払いオプション**: 前払いなし、一部前払い、全額前払いから選択可能
- **自動適用**: 適格なリソースに自動的に割引が適用
- **共有**: AWS Organizations 内で複数のアカウント間で共有可能

## 推奨事項

1. **使用パターンの分析**

   - AWS Cost Explorer を使用して現在の使用状況を分析
   - Savings Plans 推奨事項を確認

2. **コミットメントレベルの選択**

   - 予測可能なワークロードに基づいて適切なコミットメント額を決定
   - 成長を考慮した余裕を持たせる

3. **定期的な見直し**
   - 使用状況と節約効果を定期的にモニタリング
   - 必要に応じて追加の Savings Plans を購入

## ベストプラクティス

- 最初は小規模なコミットメントから開始
- 複数の Savings Plans を組み合わせて使用
- AWS Budgets を活用して使用状況を監視
- Organizations 内での一元管理を検討

## 関連リソース

- [AWS Cost Explorer](./aws-cost-explorer.md)
- [AWS Budgets](./aws-budgets.md)
- [AWS Cost and Usage Report](./aws-cost-and-usage-report.md)

# AWS Cost Explorer

・AWS リソースのコストや使用状況を可視化し、分析を支援するためのサービス

・タグ、リソース、リージョン、アカウント等によるフィルタリング

・グラフによるレポーティング機能

・コスト予測および予約の推奨

## 主なユースケース

### 1. コスト最適化

- 使用率の低いリソースの特定
- 不要なリソースの検出と削除
- リザーブドインスタンス（RI）の活用機会の発見

### 2. 予算管理

- 月次・年次のコスト傾向分析
- 予期せぬコスト増加の早期発見
- 部門別・プロジェクト別のコスト配分

### 3. キャパシティプランニング

- 将来のコスト予測
- スケーリング計画の立案
- 長期的な投資判断のサポート

## ベストプラクティス

1. **タグ付けの徹底**

   - プロジェクト、環境、部門などの適切なタグ付け
   - コスト配分の正確な把握

2. **定期的なモニタリング**

   - 週次/月次でのコストレビュー
   - 異常値の早期発見

3. **AWS Budgets との連携**

   - 予算アラートの設定
   - コストしきい値の監視

4. **レポートの自動化**
   - 定期的なコストレポートの生成
   - 関係者への自動配信

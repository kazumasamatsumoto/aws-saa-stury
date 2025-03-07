# Amazon Managed Service for Prometheus

## 概要

Amazon Managed Service for Prometheus（AMP）は、オープンソースの Prometheus をマネージドサービスとして提供し、コンテナ化されたアプリケーションやインフラストラクチャの監視を実現するサービスです。

![AMP シナリオ](/image/management-monitoring&governance/logging-monitoring/amp-scenario.svg)

## 解決する課題

1. **データの永続化**

   - Prometheus 単体ではデータの永続保存が困難
   - 大規模データの管理が複雑
   - バックアップ運用の負担

2. **スケーラビリティ**

   - 手動でのスケーリング管理
   - リソース使用量の予測が必要
   - クラスタ管理の複雑さ

3. **高可用性**
   - マルチ AZ 構成の実現が困難
   - フェイルオーバーの複雑さ
   - 運用管理の負担

## アーキテクチャ

![AMP アーキテクチャ](/image/management-monitoring&governance/logging-monitoring/amp-architecture.svg)

## 主な機能

1. **メトリクス収集**

   - Prometheus 互換のエンドポイント
   - サービスディスカバリ
   - Remote Write API

2. **データ管理**

   - マルチ AZ ストレージ
   - 長期データ保持
   - 自動スケーリング

3. **クエリと分析**
   - PromQL サポート
   - Grafana 統合
   - カスタムダッシュボード

## 利用開始の手順

1. AMP ワークスペースの作成
2. IAM ロールと権限の設定
3. Prometheus エージェントの設定
4. メトリクス収集の開始

## ベストプラクティス

1. **効率的なメトリクス収集**

   - 適切なスクレイプ間隔
   - ラベル設計の最適化
   - カーディナリティの管理

2. **クエリ最適化**

   - 効率的な PromQL
   - 適切な時間範囲
   - キャッシュの活用

3. **コスト管理**
   - メトリクス保持期間の設定
   - サンプリングの活用
   - 不要なメトリクスの削除

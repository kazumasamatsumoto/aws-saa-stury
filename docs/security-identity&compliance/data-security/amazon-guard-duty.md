# Amazon GuardDuty

Amazon GuardDuty は、AWS リソースを保護するためのインテリジェントな脅威検出サービスです。

![Amazon GuardDuty](/image/security-identity&compliance/data-security/guard-duty-overview.svg)

## 主な特徴

1. **継続的モニタリング**

   - VPC フローログ
   - CloudTrail イベントログ
   - DNS ログ
   - Kubernetes 監査ログ

2. **機械学習による異常検知**

   - 不正なアクティビティ
   - 悪意のある動作パターン
   - 未承認の動作

3. **脅威インテリジェンス**

   - マルウェア感染
   - 不正な通信
   - データ漏洩の試み
   - クレデンシャルの悪用

4. **自動対応**
   - EventBridge との連携
   - Lambda 関数による自動修復
   - SecurityHub との統合

## 接続線の関係性説明

1. **入力ソース → GuardDuty**

   - VPC フローログ: ネットワークトラフィックの分析
   - CloudTrail ログ: API アクティビティの監視
   - DNS ログ: DNS 要求の分析

2. **GuardDuty → 出力先**
   - EventBridge: イベント検出時のトリガー
   - Security Hub: セキュリティ状態の集中管理
   - Lambda: 自動修復アクションの実行

この図では、GuardDuty を中心に置き、左側に入力ソース、右側に出力先を配置しています。各コンポーネントは明るい色調で表現し、視認性を高めています。接続線は直角に曲がる形状を採用し、データの流れを明確に示しています。

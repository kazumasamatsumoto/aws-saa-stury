# AWS Organizations の全体像

AWS Organizations の主要な目的は、一つの会社・組織が持つ複数の AWS アカウントを一元管理することです。

例えば、以下のような状況で使用されます：

1. 複数の部門や事業部がある会社で

- 開発部門の AWS アカウント
- 本番環境用の AWS アカウント
- テスト環境用の AWS アカウント
- 経理部門用の AWS アカウントなど、部門ごとに別々の AWS アカウントを持っている場合

2. これらを一つの組織として

- セキュリティポリシーの一括適用
- 請求の一元管理
- リソースの共有
- 監査ログの統合管理を実現します

全体像はこんな感じ

![AWS-Organizations](/image/management-monitoring&governance/multi-account/aws-organizations-core.svg)

## SCP

![SCP](/image/management-monitoring&governance/multi-account/scp-overview.svg)

## 一括請求管理

![Consolidated-Billing](/image/management-monitoring&governance/multi-account/consolidated-billing.svg)

## CloudFormation StackSets

![CloudFormation-StackSets](/image/management-monitoring&governance/multi-account/stacksets-overview.svg)

## CloudTrail

![CloudTrail](/image/management-monitoring&governance/multi-account/cloudtrail-integration.svg)

## Organization API

![Organization-API](/image/management-monitoring&governance/multi-account/organization-api.svg)

## AWS Control Tower Core Services

![AWSControlTowerCoreServices](/image/management-monitoring&governance/multi-account/landing-zone-core.svg)

## Landing Zone

![LandingZone](/image/management-monitoring&governance/multi-account/landing-zone-accounts.svg)

## Landing Zone とは

クラウドコンピューティングにおける「Landing Zone」は、その名前の由来となったヘリコプターの着陸地点（ヘリパッド）の概念からのメタファーとして使用されています。

以下のような類似点があります：

1. **安全な着地点**

- ヘリパッド：航空機が安全に着陸できるように準備された場所
- AWS Landing Zone：組織がクラウドを安全に利用開始できるように準備された環境

2. **標準化された構造**

- ヘリパッド：規定に従った大きさ、マーキング、安全設備を備えた標準的な構造
- AWS Landing Zone：AWS のベストプラクティスに基づいて標準化された環境構造

3. **管理された環境**

- ヘリパッド：管理者による保守、安全チェック、アクセス管理
- AWS Landing Zone：ガバナンス、セキュリティ、コンプライアンスの管理された環境

つまり、AWS Landing Zone は：

- 「組織が AWS クラウドに安全に"着地"（導入開始）するための準備された環境」
- 「クラウドジャーニーの出発点となる整備された基盤」

という意味を持っています。

ビジネスの文脈で言えば：

1. **導入の安全性**：未整備の場所に着陸するリスクを避けるように、整備されていない状態でのクラウド導入のリスクを回避
2. **標準化**：どのヘリコプターでも安全に着陸できるように、どの部門・プロジェクトでも安全にクラウドを利用可能
3. **管理の一貫性**：航空管制のように、一元的な管理とガバナンスを実現

このように、「Landing Zone」という名称には、「安全」「標準化」「管理」という重要な概念が含まれており、クラウド環境の基盤としての役割を象徴的に表現しています。

![AboutLandingZone](/image/management-monitoring&governance/multi-account/landing-zone-concept.svg)

## Service-catalog

組織のブレをなくすことができます！

![service-catalog](/image/management-monitoring&governance/multi-account/service-catalog-problems-solutions.svg)

## AWS Resource Access Manager (RAM)

AWS RAM の本質的な価値は「リソースの効率的な共有と管理の一元化」にあります。

例えば：

1. 同じような機能のリソースを各アカウントで個別に作成する必要がなくなります

   - Transit Gateway を複数アカウントで共有できる
   - サブネットを複数アカウントで共有できるなど

2. コスト面での効率化

   - 重複したリソースを作成しないため、コストを削減できる
   - 共有されたリソースの料金は所有者アカウントにのみ請求される

3. 管理面での効率化
   - 一箇所でリソースを管理できる
   - 権限管理が簡素化される
   - 各アカウントでの設定作業が不要になる

つまり、「効率的なリソース利用」に加えて、「管理の一元化」と「コスト最適化」という 3 つの主要な価値を提供するサービスと言えます。特に大規模な組織や、複数の AWS アカウントを使用している環境で真価を発揮します。

リソースの再利用性を高めることで、組織全体としての AWS 環境をより効率的に運用できるようになります。

![aws-ram](/image/management-monitoring&governance/multi-account/aws-ram-diagram.svg)

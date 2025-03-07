# AWS Identity and Access Management (IAM)

## 概要

AWS IAM（Identity and Access Management）は、AWS リソースへのアクセスを安全に管理するためのサービスです。IAM を使用することで、誰が（認証）どのリソースにどのような操作を（認可）できるかを細かく制御することができます。

![AWS-IAMの概要](/image/security-identity&compliance/iam/aws-iam.svg)

## 認証と認可の流れ

![AWS-IAM認証認可フロー](/image/security-identity&compliance/iam/aws-iam-auth-flow.svg)

### Principal（実行主体）

- AWS リソースにアクセスを要求するエンティティ
- IAM ユーザー、IAM ロール、AWS サービス、外部ユーザーなどが該当
- 各 Principal は一意の識別子を持つ

### Request（リクエスト）

- Principal からの AWS リソースへのアクセス要求
- 以下の情報を含む：
  - アクション（何をするか）
  - リソース（どのリソースに対して）
  - Principal（誰が）
  - 環境データ（いつ、どこから、など）

### Access（アクセス制御）

1. 認証（Authentication）

   - Principal の身元確認プロセス
   - ユーザー名/パスワード、アクセスキー、一時的認証情報などで実施
   - MFA による追加のセキュリティ層の提供

2. 認可（Authorization）
   - Principal が要求したアクションを実行できるか判断するプロセス
   - IAM ポリシーに基づいて評価
   - 明示的な許可が必要（デフォルトでは拒否）

## 主要な構成要素

### 1. IAM ユーザー

- 個々のユーザーを表す長期的な認証情報
- ユーザー名とパスワード、またはアクセスキーを使用して認証
- 特定の権限を割り当てることが可能

### 2. IAM グループ

- IAM ユーザーの集合
- グループ単位での権限管理が可能
- ユーザーは複数のグループに所属可能

### 3. IAM ロール

- 一時的な認証情報を提供
- AWS リソース（EC2 インスタンスなど）や外部ユーザーに割り当て可能
- 特定の権限セットを定義

### 4. IAM ポリシー

- JSON 形式で記述された権限の定義
- リソースへのアクセス許可/拒否を詳細に制御
- ユーザー、グループ、ロールに付与可能

## セキュリティのベストプラクティス

### ルートユーザー

- AWS アカウント作成時に自動的に作成される特権ユーザー
- アカウントの全リソースに対するフルアクセス権限を持つ
- 制限や権限の変更が不可能

#### ルートユーザーでのみ実行可能な操作

- AWS アカウントの設定変更
- IAM ユーザーのパスワードポリシーの変更
- AWS アカウントの解約
- AWS Support プランの変更
- AWS Organizations の管理アカウントとしての組織作成
- S3 バケットの所有者としてのバケット所有者の変更
- Route 53 のドメイン登録の解約

#### ルートユーザーのセキュリティ対策

1. 日常的な作業には使用しない

   - 代わりに必要な権限を持つ IAM ユーザーを作成して使用

2. 強力なパスワードの設定

   - 最低 16 文字以上の複雑なパスワードを使用

3. MFA の必須化

   - ハードウェアまたはソフトウェア MFA デバイスを設定
   - U2F セキュリティキーの使用を推奨

4. ルートユーザーの認証情報を安全に保管

   - パスワードと MFA デバイスは別々に保管
   - 組織内で適切に管理・共有

5. アクセスキーの削除

   - ルートユーザーのアクセスキーは作成しない
   - 既存のアクセスキーは削除

6. 定期的なセキュリティ監査

   - ルートユーザーの使用履歴を確認
   - 不正アクセスの早期発見

7. 最小権限の原則を適用

   - 必要最小限の権限のみを付与

8. MFA の有効化

   - 重要なアカウントに対して多要素認証を設定

9. 認証情報の定期的な更新

   - アクセスキーやパスワードを定期的にローテーション

10. IAM ポリシーの定期的な見直し

    - 不要な権限を削除し、セキュリティを最適化

## モニタリングとログ

- AWS CloudTrail と統合して IAM の使用状況をログ記録
- IAM Access Analyzer による権限の分析
- AWS Config による設定変更の追跡

## クロスアカウントアクセス管理

### 概要

クロスアカウントアクセスとは、異なる AWS アカウント間でのリソースアクセスを可能にする機能です。組織で複数の AWS アカウントを運用する場合に、セキュアな方法でリソース共有を実現できます。

### 実装方法

1. IAM ロールを使用したアクセス委譲

   - リソースを所有するアカウント（信頼されるアカウント）で IAM ロールを作成
   - 信頼ポリシーで、アクセスを許可するアカウント（信頼するアカウント）を指定
   - アクセス権限を IAM ロールにアタッチ

2. リソースベースのポリシー
   - S3 バケットポリシーなど、リソース側で直接他アカウントへの許可を定義
   - Principal 要素で特定の AWS アカウントや IAM ユーザーを指定可能

### クロスアカウントポリシーの例

#### 信頼ポリシーの例

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::123456789012:root"
      },
      "Action": "sts:AssumeRole",
      "Condition": {}
    }
  ]
}
```

#### S3 バケットポリシーの例

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::123456789012:user/username"
      },
      "Action": ["s3:GetObject", "s3:ListBucket"],
      "Resource": [
        "arn:aws:s3:::example-bucket",
        "arn:aws:s3:::example-bucket/*"
      ]
    }
  ]
}
```

1. 最小権限の原則

   - 必要最小限の権限のみを付与
   - 定期的な権限の見直しと不要な権限の削除

2. 条件付きアクセス

   - IP アドレス制限
   - MFA 認証の要求
   - アクセス時間の制限

3. アクセスのモニタリング

   - CloudTrail でのクロスアカウントアクティビティの監視
   - 異常検知の設定

4. 一時的な認証情報の使用
   - 長期的な認証情報の代わりに STS を使用
   - セッション期間の適切な設定

## Permissions Boundary（アクセス権限の境界）

### 概要

Permissions Boundary は、IAM エンティティ（ユーザーまたはロール）に付与できる最大の権限を設定する機能です。これにより、組織内での権限の過剰付与を防ぎ、セキュリティを強化することができます。

### 主な特徴

1. 権限の上限設定

   - エンティティに付与できる最大権限を定義
   - 実効権限は、アイデンティティベースポリシーと Permissions Boundary の共通部分

2. 委任された管理
   - 開発者に IAM ユーザー作成権限を付与しつつ、作成できるユーザーの権限を制限
   - 権限管理の分散化を安全に実現

### 設定例

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:*", "cloudwatch:*", "ec2:Describe*"],
      "Resource": "*"
    },
    {
      "Effect": "Deny",
      "Action": ["iam:*", "organizations:*"],
      "Resource": "*"
    }
  ]
}
```

### 利用シナリオ

1. 開発環境での権限管理

   - 開発者に必要な権限を付与しつつ、重要なサービスへのアクセスを制限
   - テスト用リソースの作成を許可しながら、本番環境への影響を防止

2. マルチテナント環境

   - 顧客ごとのワークスペース内での権限を制限
   - リソースの分離を確実に実施

3. 組織の権限管理
   - 部門やチーム単位での権限境界を設定
   - コンプライアンス要件への対応

### ベストプラクティス

1. 階層的な権限設計

   - 組織構造に合わせた権限境界の設定
   - 部門やプロジェクト単位での権限制御

2. 定期的な見直し

   - 権限境界の適切性を定期的に評価
   - 必要に応じて境界の調整を実施

3. 監査とモニタリング
   - 権限境界の変更を追跡
   - 違反や異常なアクセスパターンの検出

## スイッチロール

### 概要

スイッチロールとは、AWS Management Console 上で一時的に別の IAM ロールに切り替えてアクセス権限を変更する機能です。クロスアカウントアクセスを実現する主要な方法の一つとして利用されます。

### 動作の仕組み

1. 認証フロー

   ![スイッチロールの認証フロー](/image/security-identity&compliance/iam/switch-role-flow.svg)

   1. ユーザーが AWS Management Console でスイッチロールを選択
   2. AWS STS（Security Token Service）が一時的な認証情報を発行
   3. 新しいロールでのセッションが開始

2. 実行時の処理

   - 元のアカウントの認証情報は維持したまま、新しいロールの権限を取得
   - コンソール上部に現在使用中のロール名が表示
   - セッションタイムアウトまたは手動での切り替えで元の権限に戻る

### 利用手順

1. 準備作業

   - 信頼されるアカウント（切り替え先）で IAM ロールを作成
   - ロールの信頼ポリシーで、信頼するアカウント（切り替え元）を指定
   - ロールに必要な権限ポリシーをアタッチ

2. スイッチロールの実行

   ```text
   1. AWSコンソールの右上にあるアカウントメニューを選択
   2. [ロールの切り替え]を選択
   3. アカウントID、ロール名、表示名を入力
   4. [切り替え]ボタンをクリック
   ```

### 主な用途

1. マルチアカウント環境の管理

   - 本番環境と開発環境の分離管理
   - 各環境へのアクセス制御を明確化

2. 特権アクセスの制御

   - 通常は最小権限で作業
   - 必要な時だけ管理者権限に切り替え

3. 一時的なアクセス権限の付与

   - 監査作業時の一時的なアクセス許可
   - プロジェクト期間中の限定的な権限付与

### セキュリティ上の利点

1. 最小権限の原則の実践

   - 通常時は必要最小限の権限で運用
   - 必要な時だけ高い権限を使用

2. アクセスの追跡性向上

   - CloudTrail でロールの切り替えを記録
   - 誰がいつどのロールを使用したか把握可能

3. 認証情報の安全な管理

   - 長期的な認証情報の共有が不要
   - 一時的な認証情報による安全なアクセス

### ベストプラクティス

1. ロール名の命名規則

   - 目的や権限レベルが分かる名前を使用
   - 環境や用途による分類を明確化

2. セッション期間の適切な設定

   - デフォルトは 1 時間
   - 用途に応じて最小限の期間を設定

3. MFA の要求

   - 重要な操作を行うロールには MFA を必須化
   - セキュリティレベルの向上

4. 定期的な権限の見直し
   - 不要なロールの削除
   - 過剰な権限の修正

## AWS Security Token Service (STS)

### 概要

AWS STS は、AWS リソースへの一時的なアクセス権限を提供するサービスです。信頼されたユーザーに対して、限定された期間のみ有効な認証情報を発行します。

![AWS-STS概要](/image/security-identity&compliance/iam/aws-sts.svg)

### 認証フロー

![AWS-STS認証フロー](/image/security-identity&compliance/iam/aws-sts-flow.svg)

1. クライアントが STS にアクセストークンをリクエスト
2. STS が一時的な認証情報を生成
   - アクセスキー ID
   - シークレットアクセスキー
   - セキュリティトークン
   - 有効期限
3. クライアントが一時的な認証情報で AWS リソースにアクセス
4. 有効期限が切れると認証情報は自動的に無効化

### 主な使用シナリオ

1. フェデレーションアクセス

   - SAML 2.0 との統合
   - ウェブ ID フェデレーション
   - カスタム ID ブローカー

2. クロスアカウントアクセス

   - 異なる AWS アカウント間での一時的なアクセス
   - ロールの引き受け（AssumeRole）

3. アプリケーションセキュリティ
   - EC2 インスタンスの一時的な認証情報
   - Lambda 関数の実行権限

### API オペレーション

1. AssumeRole

   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Effect": "Allow",
         "Action": "sts:AssumeRole",
         "Resource": "arn:aws:iam::ACCOUNT-ID:role/ROLE-NAME"
       }
     ]
   }
   ```

2. AssumeRoleWithSAML

   - SAML 2.0 ベースのフェデレーション
   - オンプレミス認証との統合

3. AssumeRoleWithWebIdentity
   - OAuth/OIDC 対応の ID プロバイダーとの統合
   - モバイルアプリケーションでの認証

### セキュリティのベストプラクティス

1. トークンの有効期限設定

   - 最小限の必要時間のみ設定
   - デフォルト: 15 分〜1 時間
   - 最大: 12 時間

2. 権限の制限

   - 必要最小限の権限のみを付与
   - 条件付きアクセスの活用

3. モニタリングと監査

   - CloudTrail での API 呼び出しの記録
   - 異常な使用パターンの検出

4. トークンの安全な管理
   - 認証情報の安全な受け渡し
   - メモリ内での一時的な保持

### エラー処理とトラブルシューティング

1. 一般的なエラー

   - ExpiredToken
   - InvalidClientTokenId
   - SignatureDoesNotMatch

2. 解決方法
   - トークンの再取得
   - 認証情報の確認
   - 時刻同期の確認

### 制限事項

1. API 制限

   - リージョンごとの制限
   - アカウントごとの同時セッション数

2. トークンの制約
   - 最大有効期限
   - トークンサイズの制限

### 料金

- API 呼び出し回数に基づく課金
- フェデレーションリクエストごとの料金

## 混乱した代理問題（Confused Deputy）

### 問題の概要

混乱した代理問題は、権限を持つエンティティ（代理）が、意図しない方法で自身の権限を第三者に利用される脆弱性です。

![混乱した代理問題の例](/image/security-identity&compliance/iam/confused-deputy-problem.svg)

### ソリューション

AWS では、この問題に対して以下の方法で対策が可能です：

![混乱した代理問題の解決策](/image/security-identity&compliance/iam/confused-deputy-solution.svg)

1. `aws:SourceArn`と`aws:SourceAccount`条件キーの使用

2. External ID の使用

External ID は、クロスアカウントのロール引き受け時に追加の認証層を提供します：

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::123456789012:root"
      },
      "Action": "sts:AssumeRole",
      "Condition": {
        "StringEquals": {
          "sts:ExternalId": "unique-id-assigned-by-third-party"
        }
      }
    }
  ]
}
```

External ID の利点：

- サードパーティサービスとの安全な連携が可能
- 同じロールを複数の顧客に提供する場合でも、各顧客を一意に識別可能
- 「混乱した代理」攻撃を防止する追加のセキュリティ層として機能

使用例：

- マネージドサービスプロバイダー（MSP）が複数の顧客の AWS アカウントにアクセスする場合
- SaaS プロバイダーが顧客の AWS リソースにアクセスする場合

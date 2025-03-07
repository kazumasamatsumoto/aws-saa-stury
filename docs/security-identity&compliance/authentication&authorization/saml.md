# SAML (Security Assertion Markup Language)

SAML は、エンタープライズユーザーの認証と認可を可能にする、XML ベースのオープン標準プロトコルです。

## 概要

SAML は、以下の主要な目的で使用されます：

- シングルサインオン（SSO）の実現
- 異なるドメイン間でのユーザー認証情報の安全な交換
- セキュリティアサーションの標準化された形式での提供

## 主要なコンポーネント

SAML には以下の 3 つの主要なコンポーネントが存在します：

1. **アイデンティティプロバイダー (IdP)**

   - ユーザーの認証を行う
   - セキュリティアサーションを生成する
   - 例：AWS IAM Identity Center, Okta, Azure AD

2. **サービスプロバイダー (SP)**

   - 保護されたリソースやサービスを提供する
   - IdP からのアサーションに基づいてアクセスを許可する
   - 例：AWS Management Console, Salesforce

3. **SAML アサーション**
   - ユーザーの身元と属性に関する情報を含む XML ドキュメント
   - デジタル署名により改ざんを防止

## SAML の構成要素

### 1. プロトコルメッセージ

SAML は以下の主要なメッセージタイプを使用します：

- **AuthnRequest**

  - SP から IdP へのユーザー認証要求
  - 認証方法や要求元の情報を含む

- **Response**
  - IdP から SP への認証結果の応答
  - SAML アサーションを含む

### 2. バインディング

SAML メッセージの転送方法を定義します：

- **HTTP POST バインディング**

  - HTML フォームを使用してメッセージを転送
  - ブラウザベースの SSO で一般的に使用

- **HTTP リダイレクトバインディング**
  - URL パラメータとしてメッセージを転送
  - 主に AuthnRequest に使用

### 3. プロファイル

一般的なユースケースの標準実装パターン：

- **Web ブラウザ SSO プロファイル**

  - ブラウザベースのシングルサインオン
  - 最も一般的な SAML プロファイル

- **シングルログアウトプロファイル**
  - 複数のサービスからの同時ログアウト
  - セッション終了の連携

### 4. アサーションの構造

SAML アサーションは以下の要素で構成されます：

1. **認証ステートメント**

   - ユーザーの認証方法
   - 認証時刻
   - セッション情報

2. **属性ステートメント**

   - ユーザーの属性情報
   - ロール、グループ所属
   - カスタム属性

3. **認可ステートメント**
   - アクセス権限の定義
   - リソースへのアクセス条件

### 5. セキュリティ機能

- **XML 署名**

  - メッセージの完全性を保証
  - 送信元の認証

- **XML 暗号化**
  - 機密情報の保護
  - エンドツーエンドの暗号化

## AWS での SAML 統合

AWS は以下の方法で SAML 2.0 フェデレーションをサポートしています：

1. **AWS IAM Identity Center**

   - エンタープライズ ID プロバイダーとの統合
   - マルチアカウントアクセスの一元管理
   - クラウドアプリケーションへの SSO アクセス

2. **IAM SAML プロバイダー**
   - カスタム SAML 統合の構築
   - 既存の ID プロバイダーとの直接統合
   - きめ細かなアクセス制御の実現

## SAML フロー

1. ユーザーがサービスプロバイダーにアクセスを試みる
2. SP がユーザーを IdP にリダイレクト
3. IdP がユーザーを認証
4. IdP が SAML アサーションを生成
5. ブラウザが SAML アサーションを SP に送信
6. SP がアサーションを検証しアクセスを許可

## セキュリティのベストプラクティス

- SAML 応答の署名を必ず検証する
- 適切な暗号化アルゴリズムを使用する
- セッションタイムアウトを適切に設定する
- 証明書の有効期限を監視する
- 定期的なセキュリティ監査を実施する

## 関連リソース

- [AWS IAM Identity Center ドキュメント](https://docs.aws.amazon.com/singlesignon/)
- [AWS IAM SAML 設定ガイド](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_saml.html)

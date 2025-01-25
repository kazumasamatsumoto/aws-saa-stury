# AWS Secrets Manager

![aws-secrets-manager](/image/security-identity&compliance/encryption/secret-manager.svg)

AWS Secrets Manager は、データベースの認証情報、API キー、その他の機密情報を安全に管理・配布するためのサービスです。

## 主な特徴

- **集中管理**: 機密情報を一元的に保存・管理
- **暗号化**: 保存時は常に AWS KMS を使用して暗号化
- **アクセス制御**: IAM ポリシーによる詳細なアクセス制御
- **自動ローテーション**: 認証情報の自動更新が可能
- **監査**: AWS CloudTrail と統合して監査ログを取得

## ユースケース

### データベース認証情報の管理

- RDS、Redshift、DocumentDB などのデータベース認証情報
- 自動ローテーション機能をサポート
- アプリケーションコードの変更なしで認証情報を更新可能

### アプリケーションシークレットの管理

- API キー
- OAuth トークン
- SSH キー
- その他の機密情報

## 自動ローテーション

Secrets Manager は以下のデータベースの認証情報を自動的にローテーションできます：

- Amazon RDS
- Amazon Aurora
- Amazon Redshift
- Amazon DocumentDB
- その他のデータベース（カスタムローテーション関数で対応）

## セキュリティのベストプラクティス

1. **最小権限の原則**

   - IAM ポリシーで必要最小限のアクセス権限を付与
   - リソースベースのポリシーを活用

2. **暗号化**

   - カスタマーマスターキー（CMK）を使用した暗号化
   - 必要に応じて独自の KMS キーを使用

3. **監査**
   - CloudTrail での操作ログ取得
   - シークレットへのアクセスを監視

## API の使用例

```python
import boto3
import json

def get_secret():
    session = boto3.session.Session()
    client = session.client(
        service_name='secretsmanager',
        region_name='ap-northeast-1'
    )

    try:
        secret_value = client.get_secret_value(
            SecretId='your-secret-name'
        )
        if 'SecretString' in secret_value:
            secret = json.loads(secret_value['SecretString'])
            return secret
    except Exception as e:
        raise e
```

## 料金

- シークレットの保存：月額$0.40/シークレット
- API 呼び出し：10,000 回まで無料、その後$0.05/10,000 回
- シークレットのローテーション：無料（Lambda 関数の実行コストは別途）

## 制限事項

- リージョンごとのシークレット数：制限あり（デフォルト 40,000）
- シークレットの最大サイズ：65,536 バイト
- バージョニング：100 バージョンまで保持可能

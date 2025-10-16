CakePHP 開発環境（プレースホルダ）

この `cake` ディレクトリは CakePHP アプリケーションを配置するための作業ディレクトリです。

使い方:

1) 既存の CakePHP ソースを提供している場合
   - アップロードまたは配布される zip/tar をこの `cake` フォルダに展開してください。
   - 展開後、依存関係をインストールします:

```powershell
cd .\cake
composer install
```

2) Composer で新規作成する場合

```powershell
# カレントがワークスペースのルート（例 d:\Work\Test\cakephp）であると仮定
cd .\cake
# CakePHP v4 系の例。v5 を使う場合はバージョン指定を変更します。
composer create-project --prefer-dist cakephp/app:~4.4 .
```

3) ローカルサーバーでの起動（簡易）

```powershell
# プロジェクトルートが cake フォルダ内であること
php -S localhost:8765 -t webroot
# または bin\cake が存在すれば
bin\cake server
```

注記:
- `config/app_local.php` や `.env` は環境固有の設定を含み、リポジトリに含まれないことがあります。
- ユーザーから CakePHP の配布物を受け取った場合、こちらに展開して依存関係（composer install）を実行してください。

トラブルシュートと便利なコマンド
 - テスト実行 (Windows):

```powershell
cd .\cake
vendor\bin\phpunit.bat
```

 - SQLite を開発用 DB として使うには、`config/app_local.php` にある `USE_SQLITE` 環境変数を有効にしてください。 PowerShell で一時的に有効化して起動する例:

```powershell
$env:USE_SQLITE='true'
php -S localhost:8765 -t webroot
```

 - Composer の SSL 関連エラーが出る場合の対処（Windows）:
   1. CA バンドルをダウンロードして保存します（例 `C:\cacert\cacert.pem`）
      ```powershell
      New-Item -ItemType Directory -Path 'C:\cacert' -Force
      Invoke-WebRequest -Uri 'https://curl.se/ca/cacert.pem' -OutFile 'C:\cacert\cacert.pem' -UseBasicParsing
      ```
   2. `php.ini` に以下を追記（php --ini で正しい php.ini を確認）:
      ```ini
      curl.cainfo = "C:\\cacert\\cacert.pem"
      openssl.cafile = "C:\\cacert\\cacert.pem"
      ```
   3. 必要に応じて Windows のルート証明書ストアを PEM にエクスポートして `cacert.pem` に追記することで、企業内ミドルCA を信頼チェーンに追加できます。

 - このリポジトリでは、初回セットアップ時に私がローカルで `composer create-project` を実行してアプリを作成しました。自動化スクリプトや CI を作る場合は、上記の CA 設定手順を CI 環境に反映してください。

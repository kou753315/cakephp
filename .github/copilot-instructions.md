# Copilot instructions for this CakePHP project

このリポジトリには現在ソースコードが含まれていないか、ワークスペースが空です。

以下は、この CakePHP プロジェクトで AI エージェントがすぐに生産的になれるためのガイドラインです。

- プロジェクトの目的とアーキテクチャ
  - このリポジトリは CakePHP アプリケーションを想定しています。典型的には `composer.json`, `src/`, `config/`, `templates/`, `plugins/`, `tests/` が存在します。
  - 主要コンポーネント: コントローラ (`src/Controller`)、モデル/エンティティ (`src/Model`)、テーブル (`src/Model/Table`)、ビュー/テンプレート (`templates/`) 、設定 (`config/`)、プラグイン (`plugins/`)。
  - データフロー: HTTP リクエスト → ルーティング (`config/routes.php`) → コントローラ → モデル（Table/Entity）→ ビュー。

- 開発ワークフロー（推奨コマンド）
  - 依存関係のインストール: `composer install`
  - ローカルサーバー起動: `bin/cake server`（プロジェクトに `bin/cake` が無い場合は `vendor/bin/cake`）
  - テスト実行: `vendor/bin/phpunit` または `composer test`（`phpunit.xml` または `phpunit.xml.dist` を確認）
  - コードスタイル: 一般に PHP-CS-Fixer や PHPCS が使われることがある。`composer.json` 内の scripts を確認。

- プロジェクト特有の注意点（探して発見すること）
  - 設定は通常 `config/app.php` と `config/app_local.php` に分かれる。`app_local.php` は環境固有の設定で、リポジトリに含まれない可能性がある。
  - カスタムプラグインが `plugins/` にある場合、プラグイン単位で同様の MVC 構成を持つ。
  - DB マイグレーションが存在すれば `config/Migrations/` または `migrations/` を探す。

- コード編集の具体例・パターン
  - 新しい CRUD エンドポイントを追加する場合は、`src/Controller/YourController.php` と `src/Model/Table/YourTable.php`、`templates/Your/index.php` 等を更新。
  - バリデーションルールは `src/Model/Table/YourTable.php` の `validationDefault()` で定義。
  - 依存注入やコンポーネントのロードは `initialize()` メソッド内で行う。

- 変更を加える際のチェックリスト
  1. 既存の `tests/` に対応するテストを追加/更新
  2. `composer.json` の `autoload` を壊していないか確認
  3. `config/routes.php` に新しいルートを追加する場合は衝突を避ける
  4. マイグレーションやシードを追加したら `Migrations` を更新

- 参考ファイルと検索ショートカット
  - まず `composer.json`, `config/routes.php`, `src/Controller`, `src/Model`, `templates`, `plugins`, `tests` を確認
  - 空のワークスペースが検出された場合、変更は小さく、README 追加や初期 composer ファイルの作成を提案

---

もし実際のソースが追加されていれば、より具体的なコード例（ファイルパス、関数名、既存コントラクト）をこのファイルに追記します。追加のリポジトリコンテンツを教えてください。
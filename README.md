# ✅ 本リポジトリについて

- 本リポジトリは、「Docker」+「Rails」+「Heroku」+「CircleCi」の環境をテンプレート化-を目的として作成しました。
- 本リポジトリを利用したい方は、下部の「本リポジトリを流用について」をご参照ください

<br>

# ✅ 環境

- Ruby 2.7.3
- Ruby on Rails 6.1.5
- Mysql 8
- Docker
- CircleCi（自動ビルト、テスト、デプロイ）
- Heroku

<br>

# ✅ 追加設定

- Bootstrap4 導入(yarn add jquery@3.5.1 bootstrap@4.5.3 popper.js@1.16.1)
- エラーページ実装
- タイムゾーンの設定
- 辞書機能の実装（日本語化対応）
- リアルタイムページ更新（development 環境）
  - https://yumishin.com/rails-docker/
- デバッグ設定：pry-rails（development 環境）
- RSpec 導入

  <br>

# ✅Docker 設定

## 🔴 設定ファイル

- Dockerfile
- docker-compose.yml

<br>

## 🔴 「config\database.yml」を修正

```
default: &default
  password: password
  host: db
```

<br>

# ✅Heroku 設定

## 🔴 デプロイ先

- https://dev-docker-rails6.herokuapp.com/

<br>

## 🔴 設定した環境変数（Heroku 側）

| 環境変数                 | 設定値                                       |
| ------------------------ | -------------------------------------------- |
| APP_DATABASE             | 「heroku config」で確認                      |
| APP_DATABASE_USERNAME    | 「heroku config」で確認                      |
| APP_DATABASE_PASSWORD    | 「heroku config」で確認                      |
| APP_DATABASE_HOST        | 「heroku config」で確認                      |
| RAILS_MASTER_KEY         | 「src\config\master.key」で確認              |
| RAILS_SERVE_STATIC_FILES | true（本番環境でコンパイルできるようにする） |
| RAILS_LOG_TO_STDOUT      | true（ログをより具体的に表示する）           |

<br>

## 🔴 「config\database.yml」を修正

```
production:
  <<: *default
  database: <%= ENV['APP_DATABASE'] %>
  username: <%= ENV['APP_DATABASE_USERNAME'] %>
  password: <%= ENV['APP_DATABASE_PASSWORD'] %>
  host: <%= ENV['APP_DATABASE_HOST'] %>
```

<br>

## 🔴HEROKU のタイムアウト設定を 120 秒に変更する（初期設定は、６０秒）

- https://tools.heroku.support/limits/boot_timeout

  <br>

# ✅CircleCi 設定

## 🔴 設定ファイル

- .circleci/config.yml

<br>

## 🔴 設定した環境変数（CircleCi 側）

| 環境変数        | 設定値                    |
| --------------- | ------------------------- |
| HEROKU_APP_NAME | Heroku で設定したアプリ名 |
| HEROKU_API_KEY  | HEROKU で確認             |

<br>

## 🔴 「config\database.yml」を修正

```
test:
  <<: *default
  database: app_test
  host: <%= ENV.fetch("APP_DATABASE_HOST") { 'DB' } %>
```

<br>

# ✅ 本リポジトリを流用について

## 🔴 使用方法

<br>

## 🔴 Git Clone 時の注意

Master key の再作成
<br>

# ✅ その他のコマンド

<br>

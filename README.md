# Laravel-Vue-Docker

Laravel と Vue の開発環境を Docker で構築したリポジトリになります。

## 前提

- git
- docker
- docker-compose

```bash
git --version
git version 2.25.1
docker --version
Docker version 20.10.2, build 2291f61
docker-compose --version
docker-compose version 1.27.4, build 40524192
```

## 構築される環境

- PHP 7.4.14
- Composer 2.0.8
- Laravel 6.20.14
- Laravel/ui 1.3.0
- Nginx 1.18.0
- Node 14.15.4
- npm 6.14.10
- vue 2.6.12
- mysql 8.0.23

## 使用方法

1. 以下のコマンドを実行しコンテナを構築。app には任意の名前を設定可能。

```bash
[host]git clone https://github.com/k-anagosan/laravel-vue-docker.git app
[host]cd app
[host]docker-compose up -d --build
```

2. app コンテナに入る。

```bash
[host]docker-copmose exec app bash
```

3. Laravel 含む composer のパッケージをインストール。

```bash
[app]composer install
```

4. .env ファイルを.env.example から作成

```bash
[app]cp .env.example .env
```

5. .env の APP_KEY を生成

```bash
[app]php artisan key:generate
```

6. web コンテナ内で vue 含む npm パッケージをインストール。

```bash
[host]docker-compose exec web sh
[web]cd /work/laravel
[web]npm install
```

7. laravel.log を手動で作成する

```bash
[host]cd /path/to/app/laravel/storage/logs
[host]touch laravel.log
```

8. ローカルの vscode で編集作業を行う場合はプロジェクトファイルの所有者を変更する。また、プロジェクトファイル全体の所有者を www-data とすることで php-fpm がファイル書き込みを行うための権限を付与する。

```bash
[host]cd /path/to   # プロジェクトルートの親ディレクトリへ移動
[host]sudo chown -R <ログイン中のユーザー名>:www-data app/
```

9. 一部ファイルのパーミッション変更

```bash
[host]cd /path/to/app/laravel/
[host]sudo chmod -R 775 storage/ bootstrap/cache
```

# HerokuにLaravel(PostgreSQL)をデプロイする手順


## プロジェクトファイルのPathに移動

```
cd <Project_Dir>
```

## Laravelプロジェクトファイルを作成

```
composer create-project --prefer-dist laravel/laravel <Project_Name>
```
```
cd <Project_Name>
```


## herokuへログイン

```
heroku login
```

## herokuにLaravelアプリのためのアプリを作成

herokuアプリの作成
```
heroku create <APP_NAME> --buildpack heroku/php
```

```
git init
heroku git:remote -a <APP_NAME>
git add.
git commit -m "make it better
git push heroku master
```

## Heroku Procfile の作成

```
echo "web: vendor/bin/heroku-php-apache2 public/" > Procfile
```

```js
// 更新
git add -A .
git commit -m "Add Procfile"
git push heroku master
```


## herokuアドオンにPostgreSQLを作成

```
heroku addons:create heroku-postgresql:hobby-dev
```


## DBコネクションの設定

LaravelのDBコネクション設定を一括設定
```
heroku config:set DB_CONNECTION=pgsql $(heroku config:get DATABASE_URL | awk '{print gensub(/postgres:\/\/(.+):(.+)@(.+):5432\/(.+)/, "DB_USERNAME=\"\\1\" DB_PASSWORD=\"\\2\" DB_HOST=\"\\3\" DB_DATABASE=\"\\4\"", "g")}')
```

## DBのマイグレーション

```
heroku run php artisan migrate
```

```js
// DBの初期化と初期データの挿入
heroku run php artisan migrate:refresh --seed
```

## アプリの情報を設定する

```js
heroku config:set DEBUGBAR_ENABLED=true
heroku config:set APP_KEY=$(php artisan --no-ansi key:generate --show)
```

## ターミナルからherokuアプリを開く

```
heroku open
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2NDg5NDY3MF19
-->
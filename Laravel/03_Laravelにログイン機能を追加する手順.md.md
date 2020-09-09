# Laravelにログイン機能を追加する手順


## Laravel6以上で認証機能を実装する

laravel/ui を composer で追加する
```
composer require laravel/ui --dev
```

artisanコマンドで好きなパッケージをインストール
```js
// Bootstrap
php artisan ui bootstrap

// Vue.js
php artisan ui vue

// React
php artisan ui react
```

```js
// --authを追加する
php artisan ui react --auth
```

npmでインストールとビルドの実行

```
npm install
npm run dev
```

DBのマイグレーション

```js
// 忘れてたら
heroku run php artisan migrate
```

## 補足:コンパイルエラーが出た場合

### cross-env : not found が出た場合

`cross-env: not found` が出た場合、
/package.json ファイルの cross-env.js のパスを修正する。

`cross-env → node_modules/cross-env/src/bin/cross-env.js`

```js
"scripts": {
        "dev": "npm run development",
        "development": "node_modules/cross-env/src/bin/cross-env.js NODE_ENV=development node_modules/webpack/bin/webpack.js --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js",
        "watch": "npm run development -- --watch",
        "watch-poll": "npm run watch -- --watch-poll",
        "hot": "/node_modules/cross-env/src/bin/cross-env.js NODE_ENV=development node_modules/webpack-dev-server/bin/webpack-dev-server.js --inline --hot --config=node_modules/laravel-mix/setup/webpack.config.js",
        "prod": "npm run production",
        "production": "/node_modules/cross-env/src/bin/cross-env.js NODE_ENV=production node_modules/webpack/bin/webpack.js --no-progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js"
    },
```

> バージョンによって cross-env.js のパスが変わっている可能性があるのでその都度 find する

### Attribute [auth] does not exist.  が出た場合

laravel/ui のバージョンを 2.0 にする
```
composer require laravel/ui "^2.0"
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA5NjA0MjU5N119
-->
# 環境構築手順
1. プロジェクトを置きたいディレクトリに移動
```
cd hoge
```

2. リポジトリをクローンする
```
git clone https://github.com/rixonmark2/laravel-docker-test.git
```

3. クローンしたプロジェクトに移動
```
cd laravel-docker-test
```

4. Dockerコンテナを起動する
```
docker-compose up -d --build
```

5. appコンテナにログイン
```
docker-compose exec app bash
```

6. vendorディレクトリにライブラリ群をインストール
```
composer install
```

7. 「.env.example」をコピーし「.evn」を作成
```
cp .env.example .env
```

8. アプリケーションキーを生成
```
php artisan key:generate
```

9. 「public/storage」から「storage/app/public」へのシンボリックリンクを張る
```
php artisan storage:link
```

10. マイグレーション実行
```
php artisan migrate
```

11. [ローカルホスト](http://127.0.0.1:8080/)にアクセスし確認
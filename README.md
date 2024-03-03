```bash
cp .env.example .env # Laravel用のenv
cd infrastructure/local
cp .env.example .env # 起動用のenv
vim .env # port書き換え
docker compose up -d

# アプリ設定
docker compose exec php-apache bash
$ composer install
$ php artisan key:generate
# DB接続確認
$ php artisan tinker
> DB::select('select 1');
= [
    {#6209
      +"?column?": 1,
    },
  ]
```

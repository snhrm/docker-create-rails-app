# dockerでrails環境構築

[rubyのDockerfile作成](Dockerfile)

### Gemfileを作成
```
$ touch Gemfile
$ touch Gemfile.lock
$ vi Gemfile

source 'https://rubygems.org'
gem 'rails', '5.2.3'
```

### dockerを起動して`rails new`しアプリケーション作成
[docker-compose.yml作成](docker-compose.yml)
```
$ docker-compose run --rm rails rails new . --force --database=mysql
```

### `database.yml`の設定
```
$ vim config/database.yml

default: &default
  adapter: mysql2
  encoding: unicode
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: <%= ENV.fetch('DATABASE_USER') { 'root' } %>
  password: <%= ENV.fetch('DATABASE_PASSWORD') { 'password' } %>
  host: <%= ENV.fetch('DATABASE_HOST') { 'localhost' } %>
  port: <%= ENV.fetch('DATABASE_PORT') { 3306 } %>

```
### 初期設定
```
docker-compose run rails bin/setup
```

### 起動
```
$ docker-compose up
```

### マイグレーション
```
docker-compose run spring spring rake db:migrate
```

### console / rake
```
docker-compose run spring spring rails console

docker-compose run spring spring rake -T
```


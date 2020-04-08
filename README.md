# Dockerで環境構築サンプル
DockerでRailsでの最低限の環境構築をしたファイルを用意しました。
データベースのMySQLを使う設定にしています。


Github使うときは`git clone`後自分のリポジトリに変更してください。

## リモート先確認

```
git remote -v
```

```
origin    https://xxxxxx.xxx/xxxxx (fetch)
origin    https://xxxxxx.xxx/xxxxx (push)
```

## 自分のリポジトリのURL貼り付けてください。

```
git remote set-url origin [変更先のURL]
```


# 使い方
1. クローンしたディレクトリに移動
2. docker-compose.ymlというファイル置いてあるディレクトリに移動
3. コマンド`docker-compose build`
4. コマンド`docker-compose up -d`
5. アプリで使うDBを作成。webのコンテナにはいる。`docker container exec -it rails-mysql_web_1 bash`と入力する
6. `app_name# rails db:create`で作成後 `app_name# exit`で抜ける
7. ブラウザで`localhost:3000`とURL欄に入力すればアプリにアクセスできる

## rails でコマンド使いたい時

```
docker container exec -it rails-docker_web_1 bash
```

rails-docker_web_1 bashがコンテナの名前になります。

これでrailsのアプリが入っているコンテナの中に入れるのでコマンドを打つことできます。

```
/app_name#
```
抜けたいとき

```
/app_name# exit
```

ついでに、Railsのサーバーは`docker-compose up -d`していると動いているので
`rails s`はいりません。
`docker-compose up`だと一つコンソールを占有します。
`-d`つけるとバックグラウンドで動作します。ログなどを見たい場合には`docker-compose up`使っても良いです。
ただし、`ctrl＋c`は禁止。正常に終了せずに次起動した時に面倒なことになることがあります。
`rails-docker/tmp/pids/server.pid`を削除すると収まる場合あるようです。

## 止める時
面倒だけどPCの電源切るときは止めておいた方がいいと思います。

```
docker-compose stop
```

## 再度開始するとき

```
docker-compose start
```

## コンテナ消したいとき
いらないコンテナあるとそれなりにPCの要領食いますので消しましょう。
あと、間違った時など

```
docker-compose down
```
オプションで--rmi allつけるとイメージも消せます。


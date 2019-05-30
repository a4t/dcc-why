# dcc-why

## これは？
docker-composeが思わぬ挙動をしたのでとりあえずpushしておいた

## 検証コマンド

```
$ git pull https://github.com/a4t/dcc-why.git
$ cd dcc-why
$ docker pull nginx
$ docker tag nginx dcc-why_app
$ docker-compose up -d app
$ docker-compose ps
    Name              Command          State   Ports
-----------------------------------------------------
dcc-why_app_1   nginx -g daemon off;   Up      80/tcp
```

docker-compose.yamlでDockerfile指定しているのにnginxが立ち上がってくる

期待している動きはbusybox内でsleepが実行されること

## アーキテクチャの話

docker-composeはdockerをラッピングしているだけなのでimege名しか見ていない

docker-composeは状態を持っているわけではないのでDockerfileの内容は知らない

わかるのはimageが存在するかどうかだけ

つまり、docker-compose build appすれば解決

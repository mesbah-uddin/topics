---
toc: false
layout: post
description: よく使うDockerコマンド一覧
categories: [markdown]
title: Dockerコマンドたち
---

ここでは、よく使うDockerコマンド一をご紹介します。詳細については、[コマンドライン・リファレンス](https://docs.docker.jp/engine/reference/commandline/toc.html)などでご確認ください。

---
## **Docker本体用コマンド**
### **docker systemでDocker本体を管理**
- 停止中のコンテナやdanglingなイメージなど不要なリソースを全て削除します。
  ```shell
  docker system prune
  ```
--- 
## **Dockerイメージ用コマンド**
### **docker buildでDockerイメージを作成**
- 現在のディレクトリにあるDockerfileという名前のDockerfileからfooというコンテナのイメージを作成します。
  ```shell
  docker build -t foo .
  ```
### **docker imagesでDockerイメージの一覧を表示**
- Dockerイメージの一覧を表示します。
  ```shell
  docker images
  ```
### **docker rmiでDockerイメージを削除**
- fooという名前のイメージを削除します。
  ```shell
  docker rmi foo
  ```
- danglingなイメージを全て削除します。
  ```shell
  docker rmi $(docker images -f “dangling=true” -q)
  ```

---
## **Dockerコンテナ用コマンド**
### **docker runでコンテナを作成（実行）**
- ubuntuのイメージをもとにコンテナを起動して、現在の日時を表示させます。
  ```shell
  docker run ubuntu /bin/date
  ```
- nginxのイメージをもとに、コンテナをバックグラウンド（デーモン）で起動します。
  ```shell
  docker run -d nginx
  ```
- nginxのstableイメージをもとに、コンテナをバックグラウンドで起動します。stableなどタグ指定のないときにlatestイメージが利用されます。
  ```shell
  docker run -d nginx:stable
  ```
- nginxのイメージをもとに、fooという名前のコンテナをバックグラウンドで起動します。
  ```shell
  docker run -d --name foo nginx
  ```
- nginxのstableイメージをもとに、webという名前のコンテナをバックグラウンドで起動し、ホストPC localhostの8080ポート宛のアクセスを、コンテナの80ポートに転送します。
  ```shell
  docker run -d -p 8080:80 --name web nginx:stable
  ```
### **docker execで稼働中のコンテナでコマンドを実行**
- webという名前の稼働中のコンテナにコマンドを実行してディレクトリ・ファイル一覧を表示します。
  ```shell
  docker exec web /bin/ls
  ```
- webという名前の稼働中のコンテナにログインします。
  ```shell
  docker exec -it web /bin/bash
  ```
### **docker logsでログを取得**
- webというコンテナ名のコンテナのログを取得します。 
  ```shell
  docker logs web
  ```
### **docker psで稼働中のコンテナ一覧を表示**
- 稼働中のコンテナの一覧を表示します。
  ```shell
  docker ps
  ```
- 停止中のコンテナも含めて全てのコンテナの一覧を表示します。
  ```shell
  docker ps -a
  ```
### **docker stopで稼働中のコンテナを停止**
- webという名前の稼働中のコンテナを停止します。
  ```shell
  docker stop web
  ```
- 稼働中のコンテナを全て停止します。
  ```shell
  docker stop $(docker ps -q)
  ```
### **docker startで停止中のコンテナを開始**
- webという名前のコンテナを再開します。
  ```shell
  docker start web
  ```
### **docker restartで稼働中のコンテナを再開**
- webという名前のコンテナを再開します。
  ```shell
  docker restart web
  ```
### **docker rmで停止中のコンテナを削除**
- 停止中のwebというコンテナを削除します。
  ```shell
  docker rm web
  ```
- 停止中コンテナを全て削除します。 
  ```shell
  docker rm $(docker ps -aq)
  ```

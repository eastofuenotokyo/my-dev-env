# my-dev-env
よく使う開発環境の構築用のファイル群。PCのDocker Desktopと連携して使います。

## 1 PCの事前準備（Windows10/Windows11の場合）
- WSL2を使えるようにする。（「Windowsの機能の有効化または無効化」から実施）
- WSL2を使用してLinuxをインストールする。
- Docker Desktopをインストールする。

## 2 開発環境構築手順
### 2-1 Python3
1. 実行に必要なpythonのライブラリがあるならば、requirements.txtに記載する。
2. Python3のソースはsrc_localフォルダ配下に格納する。 
3. 最低限の実行コマンドは以下の通り。
```
# イメージ構築・コンテナ構築・コンテナ起動。
docker compose up -d

# Linuxコマンドを使用して.pyファイルを実行。何かをファイル出力する。bashの終了。
docker compose exec python3 bash
python src_container/test.py
echo test > src_container/out.txt
exit

# コンテナ停止・コンテナ破棄・イメージの破棄。
docker compose down
docker image rm python3-image
```

### 2-2 MySQL
```
# イメージ構築・コンテナ構築・コンテナ起動。
docker compose up -d

# Linuxコマンドを使用してMySQLにログイン。mydbというデータベースを作成。
docker compose exec db bash
mysql -u root -p12345678
create database mydb;
quit
exit

# A5:SQL mk-2を使用して外部から接続する場合。
#   IPアドレスをWSL2側で調べて接続先に指定する必要がある。
#   localhostを指定するのは誤り。

# コンテナ停止・コンテナ破棄・イメージの破棄。
docker compose down
docker image rm mysql_db
```

### 2-3 Apache
1. htdocsフォルダ配下にWebサーバに配置する資源を格納する。あとから置いても構わない。
2. コマンドを実行する。

```
# イメージ構築・コンテナ構築・コンテナ起動。
docker compose up -d

# Windows側のブラウザから表示確認をする。 http://localhost:8080/

# コンテナ停止・コンテナ破棄・イメージの破棄。
docker compose down
docker image rm apache_httpd
```

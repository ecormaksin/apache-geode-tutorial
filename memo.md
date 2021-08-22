# Memo

下記URLの手順に関するメモ。

https://cwiki.apache.org/confluence/display/GEODE/Index#Index-Geodein5minutesGeodein5minutes

`docker run -it apachegeode/geode` で Docker のコンテナを起動してサンプルコードを実行すると、以下のエラーが発生した。

```
Exception in thread "main" org.apache.geode.cache.client.NoAvailableLocatorsException: Unable to connect to any locators in the list [HostAndPort[2cf32cc1ad1a/<unresolved>:10334], HostAndPort[localhost/<unresolved>:10334]]
```

- 解決の参考になったページ: https://ashishtechmill.com/connecting-a-java-client-with-apache-geode-docker-container
- 関連する公式ページのドキュメント: https://geode.apache.org/docs/guide/13/tools_modules/gfsh/command-pages/start.html#topic_591260CF25D64562A0EDD7260D2AC6D4


- Docker コンテナ起動時のコマンド

```shell
docker run -it \
  --name apache-geode-tutorial-server \
  -p 1099:1099 \
  -p 7070:7070 \
  -p 8080:8080 \
  -p 10334:10334 \
  -p 40404:40404 \
  apachegeode/geode
```

- コンテナ起動後のコマンド

```shell
start locator --hostname-for-clients=localhost
start server --hostname-for-clients=localhost
create region --name=hello --type=REPLICATE
```

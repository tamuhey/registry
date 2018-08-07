# Docker Container Private Registry

## 事前準備事項


### hostsファイルへの登録

自己署名証明書のドメイン名で、レジストリサーバーをアクセスできる様に、
パソコンのhostsファイルに次のエントリを追加します。

~~~
192.168.1.25  private.registry.local
~~~


###  自己署名証明書の登録 macOS

自己署名証明書のエラーを回避するため、自己署名証明書をMacのキーチェーンへ登録します。


1. キーチェーンアクセスを起動して、以下を選択する
　　-> キーチェーン:システム
　　-> 分類:証明書

2. auth/domain.crt ファイルを キーチェーンの証明書リストへ、ドラッグ＆ドロップ

3. piravate.registry.local をクリック

4. ポップアップしたウィンドの「信頼」を展開
   そして、この証明書を利用する時: 「常に信頼」を選択

5. Dockerを再起動




## レジストリの開始

~~~
docker-compose up -d
~~~


レジストリへログイン

~~~
$ docker login -u=dockman -p=qwerty private.registry.local:5043
~~~


コンテナのPush

~~~
$ docker tag ubuntu:latest private.registry.local:5043/ubuntu:latest
$ docker push private.registry.local:5043/ubuntu:latest
~~~


コンテナの実行

~~~
$ docker run -it private.registry.local:5043/ubuntu:latest bash
root@f2c28a25bf10:/# ps
  PID TTY          TIME CMD
    1 pts/0    00:00:00 bash
    9 pts/0    00:00:00 ps
~~~


## レジストリの停止

~~~
docker-compose down
~~~




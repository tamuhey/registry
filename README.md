# Docker Container Private Registry


## レジストリの開始

~~~
docker-compose up -d
~~~


レジストリへログイン

~~~
docker login -u=testuser -p=testpassword private.registry.local:5043
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




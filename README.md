docker-ce
^^^^^^^^^^^^^^^^^^^^^^^

1. CentOS用docker-ceインストール

| playbook名： docker-ce/docker-ce_site.yml
| 本PlaybookはCentOSにdocker-ceをインストールする際に使用します。
| インストールにあたって引数は必要としません。
| 

2. CentOS用docker-composeインストール

| playbook名： docker-compose/docker-compose_site.yml
| 本PlaybookはCentOS用docker-ceにdocker-composeをインストールする際に使用します。
| 以下引数を必要とします。
| 

    * docker_compose_ver: 
            Docker-composeのバージョンを指定します。


| サンプル

.. code-block:: none

    docker_compose_ver: 1.17.1



3. dockerに外部からアクセスするための設定

| playbook名： accept_remote_access/accept_remote_access_site.yml
| 本PlaybookはCentOS用docker-ceの外部アクセス用Portを開放し、外部からのアクセスを可能とする際に使用します。
| 以下引数を必要とします。
| 

    * access_port:
            アクセスを待ち受けるPort番号を記載します。デフォルトは2375です。
    * access_ip: 
            アクセスを待ち受けるIPアドレスを記載します。0.0.0.0とすることでどのIPアドレス宛でも受け付けます。
    * access_from: 
            dockerの起動ファイル時の引数として、起動ファイル内に記載する内容を記載します。


| サンプル

.. code-block:: none

    access_port: 2375
    access_ip: 0.0.0.0
    access_from: "-H tcp://{{ access_ip }}:{{ access_port }} -H unix://var/run/docker.sock"



4. Ansibleからの操作を受け付けるようにするための設定

| playbook名： enable_access_from_ansible/enable_access_from_ansible_docker-ce_site.yml
| 本PlaybookはCentOS用docker-ceをAnsibleから使用するにあたって必要となるモジュールのインストールをする際に使用します。
| インストールにあたって引数は必要としません。
| 

5. コンテナ作成

| playbook名： deploy/deploy_container_site.yml
| 
| 本Playbookはdockerサーバ上にコンテナを作成する際に使用します。
| 以下引数を必要とします。
| 

    * need_local_volume:
            コンテナ作成時にdockerサーバのローカル領域にディレクトリを作成するかしないかの設定。yesの場合は作成します。
    * localvolumes:
            作成するローカルディレクトリを羅列します。複数ある場合を想定し、"- path"のように記載します。
    * containersettings:
            各コンテナに関する設定を記載します。複数ある場合を想定し、"- {各設定値}"のように記載します。

        - container_name:
                コンテナの名前（タグ名）を指定します。インベントリー名と一致させます。
        - container_image:
                コンテナ作成時に使用するdockerのイメージファイルを指定します。
        - container_ports:
                dockerサーバのPortとコンテナ内のPortを紐づけます。複数ある場合を想定し、[]内に記載します。
        - container_volumes:
                dockerサーバのディレクトリとコンテナ内のディレクトリを紐づけます。複数ある場合を想定し、[]内に記載します。

| サンプル

.. code-block:: none

    need_local_volume: "yes"
    localvolumes:
    - /data/elasticsearch/data
    - /data/elasticsearch/env
    - /data/elasticsearch/conf
    - /data/elasticsearch/log
    containersettings:
    - {"container_name": "esmaster01", "container_image": "centos", "container_ports": [ "9200:9200", "9300:9300", "9201:9201"], "container_volumes": [ "/data/elasticsearch/conf:/etc/elasticsearch", "/data/elasticsearch/env:/etc/sysconfig/elasticsearch", "/data/elasticsearch/data:/var/lib/elasticsearch", "/data/elasticsearch/log:/var/log/elasticsearch"]}

docker-ce
^^^^^^^^^^^^^^^^^^^^^^^

1. CentOS�pdocker-ce�C���X�g�[��

| playbook���F docker-ce/docker-ce_site.yml
| �{Playbook��CentOS��docker-ce���C���X�g�[������ۂɎg�p���܂��B
| �C���X�g�[���ɂ������Ĉ����͕K�v�Ƃ��܂���B
| 

2. CentOS�pdocker-compose�C���X�g�[��

| playbook���F docker-compose/docker-compose_site.yml
| �{Playbook��CentOS�pdocker-ce��docker-compose���C���X�g�[������ۂɎg�p���܂��B
| �ȉ�������K�v�Ƃ��܂��B
| 

    * docker_compose_ver: 
            Docker-compose�̃o�[�W�������w�肵�܂��B


| �T���v��

.. code-block:: none

    docker_compose_ver: 1.17.1



3. docker�ɊO������A�N�Z�X���邽�߂̐ݒ�

| playbook���F accept_remote_access/accept_remote_access_site.yml
| �{Playbook��CentOS�pdocker-ce�̊O���A�N�Z�X�pPort���J�����A�O������̃A�N�Z�X���\�Ƃ���ۂɎg�p���܂��B
| �ȉ�������K�v�Ƃ��܂��B
| 

    * access_port:
            �A�N�Z�X��҂��󂯂�Port�ԍ����L�ڂ��܂��B�f�t�H���g��2375�ł��B
    * access_ip: 
            �A�N�Z�X��҂��󂯂�IP�A�h���X���L�ڂ��܂��B0.0.0.0�Ƃ��邱�Ƃłǂ�IP�A�h���X���ł��󂯕t���܂��B
    * access_from: 
            docker�̋N���t�@�C�����̈����Ƃ��āA�N���t�@�C�����ɋL�ڂ�����e���L�ڂ��܂��B


| �T���v��

.. code-block:: none

    access_port: 2375
    access_ip: 0.0.0.0
    access_from: "-H tcp://{{ access_ip }}:{{ access_port }} -H unix://var/run/docker.sock"



4. Ansible����̑�����󂯕t����悤�ɂ��邽�߂̐ݒ�

| playbook���F enable_access_from_ansible/enable_access_from_ansible_docker-ce_site.yml
| �{Playbook��CentOS�pdocker-ce��Ansible����g�p����ɂ������ĕK�v�ƂȂ郂�W���[���̃C���X�g�[��������ۂɎg�p���܂��B
| �C���X�g�[���ɂ������Ĉ����͕K�v�Ƃ��܂���B
| 

5. �R���e�i�쐬

| playbook���F deploy/deploy_container_site.yml
| 
| �{Playbook��docker�T�[�o��ɃR���e�i���쐬����ۂɎg�p���܂��B
| �ȉ�������K�v�Ƃ��܂��B
| 

    * need_local_volume:
            �R���e�i�쐬����docker�T�[�o�̃��[�J���̈�Ƀf�B���N�g�����쐬���邩���Ȃ����̐ݒ�Byes�̏ꍇ�͍쐬���܂��B
    * localvolumes:
            �쐬���郍�[�J���f�B���N�g���𗅗񂵂܂��B��������ꍇ��z�肵�A"- path"�̂悤�ɋL�ڂ��܂��B
    * containersettings:
            �e�R���e�i�Ɋւ���ݒ���L�ڂ��܂��B��������ꍇ��z�肵�A"- {�e�ݒ�l}"�̂悤�ɋL�ڂ��܂��B

        - container_name:
                �R���e�i�̖��O�i�^�O���j���w�肵�܂��B�C���x���g���[���ƈ�v�����܂��B
        - container_image:
                �R���e�i�쐬���Ɏg�p����docker�̃C���[�W�t�@�C�����w�肵�܂��B
        - container_ports:
                docker�T�[�o��Port�ƃR���e�i����Port��R�Â��܂��B��������ꍇ��z�肵�A[]���ɋL�ڂ��܂��B
        - container_volumes:
                docker�T�[�o�̃f�B���N�g���ƃR���e�i���̃f�B���N�g����R�Â��܂��B��������ꍇ��z�肵�A[]���ɋL�ڂ��܂��B

| �T���v��

.. code-block:: none

    need_local_volume: "yes"
    localvolumes:
    - /data/elasticsearch/data
    - /data/elasticsearch/env
    - /data/elasticsearch/conf
    - /data/elasticsearch/log
    containersettings:
    - {"container_name": "esmaster01", "container_image": "centos", "container_ports": [ "9200:9200", "9300:9300", "9201:9201"], "container_volumes": [ "/data/elasticsearch/conf:/etc/elasticsearch", "/data/elasticsearch/env:/etc/sysconfig/elasticsearch", "/data/elasticsearch/data:/var/lib/elasticsearch", "/data/elasticsearch/log:/var/log/elasticsearch"]}

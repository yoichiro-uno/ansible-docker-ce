InstallDockerCompose: "yes"
ExecTest: "no"
TestComposeSite: "no"
TestSingleSite: "no"
docker_compose_ver: 1.17.1

access_port: 2375
access_ip: 0.0.0.0
access_from: "-H tcp://{{ access_ip }}:{{ access_port }} -H unix://var/run/docker.sock"




need_local_volume: "yes"
localvolumes:
  - /data/apache/web01/conf
  - /data/apache/web01/log
  - /data/apache/web01/data
  - /data/apache/web02/conf
  - /data/apache/web02/log
  - /data/apache/web02/data

containersettings:
 - {"container_name": "web01", "container_image": "centos", "container_ports": [ "10080:80"], "container_volumes": [ "/data/apache/web01/conf:/etc/httpd/conf" , "/data/apache/web01/log:/var/log/httpd" ,"/data/apache/web01/data:/var/www/html"]}
 - {"container_name": "web02", "container_image": "centos", "container_ports": [ "10081:80"], "container_volumes": [ "/data/apache/web02/conf:/etc/httpd/conf" , "/data/apache/web02/log:/var/log/httpd" ,"/data/apache/web02/data:/var/www/html"]}

# Micorservices
#
#
#logging-1

$ export GOOGLE_PROJECT=docker-274114
$ docker-machine create --driver google \
    --google-machine-image https://www.googleapis.com/compute/v1/projects/ubuntu-os-cloud/global/images/family/ubuntu-1604-lts \
    --google-machine-type g1-small \
    --google-open-port 5601/tcp \
    --google-open-port 9292/tcp \
    --google-open-port 9411/tcp \
    logging

# configure local env
$ eval $(docker-machine env logging)

# узнаем IP адрес
$ docker-machine ip logging

#for elastic
docker-machine ssh
sudo sysctl -w vm.max_map_count=262144

$ bash docker_build.sh
$ bash docker_build.sh
$ bash docker_build.sh

Запушьте собранные вами образы на DockerHub:
$ docker login
Login Succeeded
$ docker push $USER_NAME/ui:logging
$ docker push $USER_NAME/comment:logging
$ docker push $USER_NAME/post:logging








Удалите виртуалку:
$ docker-machine rm vm1
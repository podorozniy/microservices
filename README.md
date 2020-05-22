# Micorservices
#
#swarm
docker-machine create --driver google \
   --google-project  docker-182408  \
   --google-zone europe-west1-b \
   --google-machine-type g1-small \
   --google-machine-image $(gcloud compute images list --filter ubuntu-1604-lts --uri) \
   master-1

docker-machine create --driver google \
   --google-project  docker-274114  \
   --google-zone europe-west1-b \
   --google-machine-type g1-small \
   --google-machine-image $(gcloud compute images list --filter ubuntu-1604-lts --uri) \
   worker-3

eval $(docker-machine env master-1)
docker-machine ssh master-1
docker swarm init
   docker swarm join-token manager/worker
docker swarm join --token SWMTKN-1-27upfa4a4imno34drva0ult6rbdnn9t8oc626t0d95hk6gr0sx-5vk86neifcvoynjoo8rq4t0b9 10.132.0.4:2377
docker node ls

docker stack deploy/rm/services/ls STACK_NAME
docker stack deploy --compose-file=<(docker-compose -f docker-compose.yml config 2>/dev/null) DEV
docker stack services DEV
docker stack ps DEV

docker service ps DEV_ui

docker node ls -q | xargs docker node inspect  -f '{{ .ID }} [{{ .Description.Hostname }}]: {{ .Spec.Labels }}'

docker inspect $(docker stack ps DEV -q --filter "Name=DEV_ui.1") --format "{{.Status.ContainerStatus.ContainerID}}"

docker stack deploy --compose-file=<(docker-compose -f docker-compose.infra.yml -f docker-compose.yml config 2>/dev/null)  DEV

export USER_NAME=podorozniy

Запушьте собранные вами образы на DockerHub:
$ docker login
Login Succeeded
$ docker push $USER_NAME/ui
$ docker push $USER_NAME/comment
$ docker push $USER_NAME/post
$ docker push $USER_NAME/prometheus
Удалите виртуалку:
$ docker-machine rm vm1

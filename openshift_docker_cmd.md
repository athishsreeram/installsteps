# Openshift & Docker Command
##  Build the docker file from location

docker build -t docker-snapshots.artifactory.com/consul-openshift:v1.6.1 .

docker image tag docker-snapshots.artifactory.com/consul-openshift:v1.6.1 docker-snapshots.artifactory.com/consul-openshift:v1.6.1


## Create new App from Docker Image
oc new-app --docker-image docker-snapshots.artifactory.com/consul-openshift:v1.6.1
oc tag consul-openshift:v1.6.1 consul-openshift:latest

## Expose Route
oc expose service consul-openshift

## No needed if doing new-app tag latest image
oc import-image --from docker-snapshots.artifactory.com/consul-openshift:v1.6.1 consul-openshift:v1.6.1 --confirm=true

## To pull from cerntal docker repo
docker login docker-snapshots.artifactory.com

docker pull docker-snapshots.artifactory.com/consul-openshift:v1.6.1

## Run Docker
docker run -it -p 8500:8500 docker-snapshots.artifactory.com/consul-openshift:v1.6.1


## Local docker Build & Tag
docker build -t consul-openshift:v1.6.1 .

docker image tag consul-openshift:v1.6.1 docker-snapshots.artifactory.com/consul-openshift:v1.6.1

## Push central Docker & Tag
docker push docker-snapshots.artifactory.com/consul-openshift:v1.6.1

docker image tag docker-snapshots.artifactory.com/consul-openshift:v1.6.1 docker-snapshots.artifactory.com/consul-openshift:latest

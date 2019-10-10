# Pre-req:
## Install Minikube
https://github.com/athishsreeram/installsteps/blob/master/minikubeinstall.md

## Install Docker
brew install docker

## Springboot Docker
https://github.com/athishsreeram/employee/blob/employee-docker/README.md

## Start:
eval $(minikube docker-env)

## Note to Undo: eval $(minikube docker-env -u).

docker build -t emp-node:v1 .

kubectl run emp-node --image=emp-node:v1 --port=8082 --image-pull-policy=Never

kubectl expose deployment emp-node --type=LoadBalancer --name=emp-node

minikube service emp-node

kubectl describe services emp-node

## Links
https://kubernetes.io/docs/reference/kubectl/cheatsheet/

https://kubernetes.io/docs/tutorials/stateless-application/expose-external-ip-address/

https://kubernetes.io/docs/reference/kubectl/cheatsheet/

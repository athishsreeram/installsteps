# Download Hyperkit
curl -LO https://storage.googleapis.com/minikube/releases/latest/docker-machine-driver-hyperkit \n && sudo install -o root -g wheel -m 4755 docker-machine-driver-hyperkit /usr/local/bin/

## Download & Install minikube
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-darwin-amd64 \n && chmod +x minikube

## Set the Profile to Dev
minikube profile dev \n

## Start the Minikube
minikube start -p dev --memory=8192 --cpus=4 \n --vm-driver=hyperkit \n --disk-size=50g \n --extra-config=apiserver.enable-admission-plugins="LimitRanger,NamespaceExists,NamespaceLifecycle,ResourceQuota,ServiceAccount,DefaultStorageClass,MutatingAdmissionWebhook"

## Create Kub Deployment
kubectl create deployment hello-node --image=gcr.io/hello-minikube-zero-install/hello-node\n

brew install watch watch -n1 kubectl get pods,svc,deployments

kubectl get events\n

kubectl config view\n

minikube service hello-node\n

minikube stop

## Help Links
https://kubernetes.io/docs/tutorials/hello-minikube/

https://kubernetes.io/docs/tasks/tools/install-minikube/

https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-on-linux

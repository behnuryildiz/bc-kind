#!/bin/bash

echo "your password needed to get worked the next issues as root to do"
su

#install from release binaries as root
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.17.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind

#we wanna see the difference betw. before and after case of the process tree. 
#first_pstree.txt creation
pstree > first_pstree.txt

#creation of a new cluster (optinal with a by own chosen name like; (--name my_cluster)
kind create cluster

#to see the created cluster
kubectl get nodes -owide

# to install the pstree command we're coming into the cluster.
docker ps -a
docker exec -it kind-control-plane bash
apt update && apt install psmisc

#after_pstree.txt creation while being in the cluster
pstree > after_pstree.txt

#execute of the kind cluster container and the compair the situation of pstree's.
diff first_pstree.txt after_pstree.txt

docker exec -it container_id bash

# in container
apt update
apt install psmisc #to be able to see the difference bet before and after 
exit

kubectl get all
kubectl config get-contexts
kubectl config use-context


#repo update and add for the prometheus app 

helm repo add any_repo_name https://prometheus-community.github.io/helm-charts

helm repo update

helm install any_repo_name prometheus-community/prometheus

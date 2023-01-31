#install from release binaries

curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.17.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind

#vor_pstree.txt creation
pstree > vor_pstree.txt

#creation of a new cluster
kind create cluster (--name my_cluster)

#nach_pstree.txt creation
pstree > nach_pstree.txt

#execute of the kind cluster container and the compair the pstree's.

diff vor_pstree.txt nach_pstree.txt

docker exec -it container_id bash

# in container
>> apt update
>> apt install psmisc #to be able to see the difference bet before and after 
>> exit

#repo update and add for the prometheus app 

helm repo add any_repo_name https://prometheus-community.github.io/helm-charts

helm repo update

helm install any_repo_name prometheus-community/prometheus

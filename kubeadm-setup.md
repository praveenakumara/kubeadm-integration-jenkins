SETUP KUBEADM CLUSTER

###################  ON MASTERNODE AND WORKER NODE  ####################
apt-get update -y

apt-get install docker.io -y

service docker restart

curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -

echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" >/etc/apt/sources.list.d/kubernetes.list

apt-get update

apt install kubeadm=1.20.0-00 kubectl=1.20.0-00 kubelet=1.20.0-00 -y

####################   ON MASTER NODE   ####################

kubeadm init --pod-network-cidr=192.168.0.0/16      ####it will create the kubeconfig file and generate the token should be paste in the worker node

#################  ON MASTER NODE   ####################

mkdir -p $HOME/.kube

sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config

sudo chown $(id -u):$(id -g) $HOME/.kube/config ### 

###################### ON MASTER NODE  ###############

kubectl apply -f https://raw.githubusercontent.com/projectcalico/calico/v3.25.1/manifests/calico.yaml

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.49.0/deploy/static/provider/baremetal/deploy.yaml


### now print the commands


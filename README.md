# Setup Kubernetes Master & Worker Node 
## Command for Master & Worker node
```
sudo su
apt-get update
```
Now install for https package
```sh
apt-get install apt-transport-https
```
Now install docker on all Master & Worker nodes
```sh
apt install docker.io -y
```
To check, Whether docker install or not
```sh
docker --version
systemctl start docker 
systemctl enable docker
```
Setup open GPG key
```sh
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb http://apt.kubernetes.io/ kubernetes-xenial main
EOF
```
install all package
```sh
apt-get update
```
Install kubelet kubeadm kubectl 
```sh
apt-get install -y kubelet kubeadm kubectl kubernetes-cni
```
# Booststraping the master node (in Master)
To inittialize k8s Cluster
```sh
kubeadm init
```
COPY THE COMMAND TO RUN IN NODES & SAVE IN NOTEPAD
Create both .kube and it's parent directories (-p)
```sh
mkdir -p $HOME/.kube
```
copy configuration to kube directory (in config file)
```sh
cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
```
Provided user permission to config file
```sh
chown $(id -u):$(id -g) $HOME/.kube/config
```
Deploy flannel node network for it's repository path 
```sh
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/k8s-manifests/kube-flannel-rbac.yml
```

# Configure Worker Node 
copy the long ocde provides my Master In Node now like code given below
```sh
e.g-kubeadm join 172.31.6.165:6443 --token kl9fhu.co2n90v3rxtqllrs --discovery-token-ca-cert-hash sha256:b0f8003d23dbf445..............
```
Go to master And run this commad 
```sh
kubectl get nodes
```


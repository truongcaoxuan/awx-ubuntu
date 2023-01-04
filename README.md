### Prereq
```
sudo apt update -y && sudo apt upgrade -y
```

### Install Minikube
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 
sudo install minikube-linux-amd64 /usr/local/bin/minikube
minikube version
```
### Install Docker
- https://docs.docker.com/engine/install/ubuntu/

```
sudo apt-get install -y ca-certificates curl gnupg  lsb-release
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
"echo \
  ""deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable"" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null"
sudo apt-get update
sudo chmod a+r /etc/apt/keyrings/docker.gpg
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
sudo usermod -aG docker $(whoami)
sudo systemctl daemon-reload
sudo systemctl enable docker
sudo systemctl start docker
sudo systemctl status docker
docker --version

hostnamectl set-hostname vm-awx
sudo reboot
```

### Install kubectl
- https://snapcraft.io/install/kubectl/ubuntu
```
sudo apt update
sudo apt install snapd
sudo snap install kubectl --classic
```

### Create MiniKube cluster
- https://minikube.sigs.k8s.io/docs/commands/start/
```
docker pull kicbase/stable:v0.0.32
docker pull gcr.io/k8s-minikube/kicbase:v0.0.32
docker pull kicbase/stable:v0.0.36
```
```
"minikube start \
--cpus=2 \
--memory=4g \
--addons=ingress \
--install-addons=true \
--base-image=""kicbase/stable:v0.0.36"" \
--kubernetes-version=v1.23.8"					
```
#### check if the minikube is ready
```
minikube kubectl -- get nodes
```
#### get all running pods from all namespaces
```
minikube kubectl -- get pods -A
```
### Deploy Awx-Operator using kustomization.yaml file
```
kustomize build . | kubectl apply -f -
```

### Install AWX v17.1.0 on Ubuntu 20.04 using Docker-compose

### Install a few prerequisite packages
```
sudo apt update -y && sudo apt upgrade -y
```

### Install Ansible
```
sudo apt install -y ansible
ansible --version
```

### Install Docker
```
sudo apt install -y docker.io
sudo usermod -aG docker $(whoami)
sudo systemctl daemon-reload
sudo systemctl enable docker
sudo systemctl start docker
sudo systemctl status docker
docker --version

hostnamectl set-hostname vm-awx
sudo reboot
```
### Install docker compose
```
sudo apt install -y docker-compose 
docker-compose --version
```
### Install AWX v17.1.0
#### clone awx
```
cd ~
git clone -b 17.1.0 https://github.com/ansible/awx.git
```
#### modify inventory file
```
cd ~/awx/installer/
sudo vi inventory
```
- admin_user=admin
- admin_password=password
```
ansible-playbook -i inventory install.yml
```




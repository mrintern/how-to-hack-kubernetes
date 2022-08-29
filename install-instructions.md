# How to Install [kube-security-lab](https://github.com/raesene/kube_security_lab)

Prefer video instructions? Check out this [tutorial video](https://www.youtube.com/watch?v=y9PbNDdtHGo&list=PLSGxDsVUZ-zyGCCYUnS5oyi54VuTQ0W4w&index=2)

## Requirements:
- (windows) ubuntu app
- kind
- docker
- ansible
- kubectl


## 0. (Windows) install ubuntu app from Microsoft store
  - install everything else from ubuntu app

## 1. Install dependencies

###  Install kubectl, kubeadmn, kubelet
  - follow these instructions carefully!
  - https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/

###  Install docker
  - linux: https://docs.docker.com/engine/install/ubuntu/#set-up-the-repository
  - mac: https://docs.docker.com/desktop/install/mac-install/
  - windows: https://docs.docker.com/desktop/install/windows-install/ simply install docker desktop on your windows machine and enable integration
  with your ubuntu app via the docker desktop settings:
![image](https://user-images.githubusercontent.com/24460340/183655409-941eb3bf-a968-4c06-bfac-60e66d5795af.png)


  

###  Install ansible
  - `sudo apt-get update`
  - `sudo apt-get install software-properties-common`
  - `sudo apt-add-repository ppa:ansible/ansible`
  - `sudo apt-get update`
  - `sudo apt-get install ansible`

###  Install kind
  - official installation guide: https://kind.sigs.k8s.io/docs/user/quick-start/#installation
  - `curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.11.0/kind-linux-amd64`
      - notice how we specify v0.11.0 here
  - `chmod +x ./kind`
  - `sudo mv ./kind /usr/bin/kind`

###  Install pip3
  - `sudo apt install python3-pip`

###  Install python3 docker module
  - `pip3 install docker`

## 2. verify installation with the following commands
  - `kubectl`
  - `kind`
  - `docker`
  - `ansible`
  - `kubeadm`

## 3. create kind cluster
  - `kind create cluster`

## 4. clone project and try running an ansible playbook
  - `git clone https://github.com/raesene/kube_security_lab.git`
  - `cd kube_security_lab`
  - `ansible-playbook insecure-port.yml`

If everything works thus far, I then you're ready to start hacking!

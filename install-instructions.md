loose instructions to launch kube_security_lab

Requirements:
- (windows) ubuntu app
- kind
- docker
- ansible
- kubectl


0. (Windows) install ubuntu app from Microsoft store
  - install everything else from ubuntu app

1. Install dependencies

##  INSTALL kubectl, kubeadmn, kubelet
  - follow these instructions carefully!
  - https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/

##  INSTALL docker
  - https://www.docker.com/products/docker-desktop/

##  INSTALL ansible
  - `sudo apt-get update`
  - `sudo apt-get install software-properties-common`
  - `sudo apt-add-repository ppa:ansible/ansible`
  - `sudo apt-get update`
  - `sudo apt-get install ansible`

##  INSTALL kind
  - `curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.11.0/kind-linux-amd64`
      - notice how we specify v0.11.0 here
  - `chmod +x ./kind`
  - `sudo mv ./kind /usr/bin/kind`

##  INSTALL pip3
  - `sudo apt install python3-pip`

##  INSTALL python3 docker module
  - `pip3 install docker`

2. verify installation with the following commands
  - `kubectl`
  - `kind`
  - `docker`
  - `ansible`
  - `kubeadm`

3. create kind cluster
  - `kind cluster create`

4. clone project and try running an ansible playbook
  - `git clone https://github.com/raesene/kube_security_lab.git`
  - `cd kube_security_lab`
  - `ansible-playbook insecure-port.yml`

If everything works thus far, I then you're ready to start hacking!

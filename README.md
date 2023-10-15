# KASM Desktop for Windows Mac Linux

- With Sound Enabled (Voice)
- https://hub.docker.com/r/linuxserver/kasm


- Workspace Settings

- Persistent profile path

- I installed ubuntu_jammy that is why I used below path

```path
/home/persistance/profiles/ubuntu_jammy/{username}
```

-  Volume Mapping
- https://kasmweb.com/docs/latest/guide/persistent_data/volume_mapping.html


- Volume Bind  # Note: This will bind the volume inside the host container ---> docker exec -it sandbox ls /mnt  ---> bind with kasm-user /mnt ---> you can bind host container with HOST MACHINE.

```json
{
  "/mnt": {
    "bind": "/mnt",
    "mode": "rw",
    "uid": 1000,
    "gid": 1000,
    "required": true,
    "skip_check": false
  }
}
```

- Login

admin: admin@kasm.local
password: password 

user: user@kasm.local
password: password

- Password Change
- Tip: open a terminal ---> sudo -i ---> passwd kasm-user ---> 1 (Incase of lock you can easily provide 
```bash
sudo passwd kasm-user
```

```bash
sudo -i
passwd kasm-user
```


### ARM64

- MAC Linux Arm

- MAC kasm arm images

```bash
docker run -id \
  --name=kasm \
  --privileged \
  --shm-size=8192m \
  -e KASM_PORT=443 \
  -p 3000:3000 \
  -p 443:443 \
  -v ${PWD}:/mnt \
  lscr.io/linuxserver/kasm:arm64v8-latest
```
- https://hub.docker.com/r/linuxserver/kasm/tags

```bash
docker run -id \
  --name=kasm-desktop \
  --shm-size=8192m \
  --privileged \
  -e KASM_PORT=443 \
  -p 3000:3000 \
  -p 443:443 \
  -v ${PWD}:/mnt \
lscr.io/linuxserver/kasm:arm64v8-1.14.0-develop
```

- kasm-user settings to add this user in sudoers groups https://kasmweb.com/docs/latest/how_to/running_as_root.html

-  Docker Run Config Override (JSON)
  ```json
{
  "hostname": "kasm",
  "privileged": true
}
```
-  Docker Exec Config (JSON)
```json
{
"first_launch": {
 "user":"root",
 "cmd":"bash -c 'apt-get update && apt-get install -y sudo && echo \"kasm-user ALL=(ALL) NOPASSWD: ALL\" >> /etc/sudoers'"
}
}
```

### AMD64

- Linux

```bash
docker run -id \
  --name=kasm \
  --privileged \
  --shm-size=8192m \
  -e KASM_PORT=8443 \
  --shm-size=8192m \
  -p 3001:3000 \
  -p 8443:8443 \
  -v ${PWD}:/mnt \
  lscr.io/linuxserver/kasm:amd64-latest
```
- Windows Power Shell --shm-size=8192m
```bash
docker run -id --name=kasm --privileged -e KASM_PORT=8443 --shm-size=8192m -p 3001:3000 -p 8443:8443 -v ${PWD}:/mnt lscr.io/linuxserver/kasm:amd64-latest
```
- https://hub.docker.com/r/linuxserver/kasm/tags
```bash
docker run -id \
  --name=kasm \
  --privileged \
  --shm-size=8192m \
  -e KASM_PORT=8443 \
  -p 3001:3000 \
  -p 8443:8443 \
  -v ${PWD}:/mnt \
  lscr.io/linuxserver/kasm:amd64-develop
```

- Windows

```bash
docker run -id --name=kasm --privileged -e KASM_PORT=443 -p 3000:3000 -p 443:443 -v "c:/users/Muhammad Asim/Desktop/sandbox:/mnt"  lscr.io/linuxserver/kasm:amd64-latest
```

- MAC kasm amd/arm images
- https://hub.docker.com/r/kasmweb/core-ubuntu-bionic/tags


- With No Sound Enabled (No Voice)
- Gui

- https://hub.docker.com/u/kasmweb

```bash
docker run --name sandbox --shm-size=4096m -v $PWD:/mnt -w /mnt -p 6901:6901 -e VNC_PW=password -id kasmweb/ubuntu-focal-desktop:1.13.1-rolling
```

```bash
docker run --name docker --shm-size=2048m -v /var/run/docker.sock:/var/run/docker.sock -v ${PWD}:/mnt -w /mnt -p 6902:6901 -e VNC_PW=password -id kasmweb/ubuntu-focal-desktop:1.13.1-rolling
```

- docker installation ---> apt update && apt install -y docker.io
- docker and docker compose installation ---> use docker script

- Ubuntu Core NoGUI
```bash
docker run --name sandbox --shm-size=4096m -v $PWD:/mnt -w /mnt -p 6901:6901 -e VNC_PW=password -id kasmweb/core-ubuntu-bionic:1.13.1
```
- Ubuntu GUI (Linux)
```bash
docker run --name sand-box --shm-size=4096m -v $PWD:/mnt -w /mnt -p 6902:6901 -e VNC_PW=password -id kasmweb/ubuntu-jammy-desktop:1.14.0-rolling
```
- Ubuntu GUI (Windows)
```bash
docker run --name sand-box --shm-size=4096m -v "c:/users/Muhammad Asim/Desktop/sandbox:/mnt" -v /var/run/docker.sock:/var/run/docker.sock -w /mnt -p 6902:6901 -e VNC_PW=password -id kasmweb/ubuntu-jammy-dind:1.14.0-rolling
```

- Ubuntu GUI (Windows)
- https://hub.docker.com/r/kasmweb/ubuntu-jammy-desktop
  
```bash
docker run --name sand-box --cpus=6 --shm-size=4096m -v /var/run/docker.sock:/var/run/docker.sock -v "c:/users/Muhammad Asim/Desktop/sandbox:/mnt" -w /mnt -p 6901:6901 -e VNC_PW=password -id kasmweb/ubuntu-jammy-desktop:1.14.0-rolling
```
- .wslconfig
```bash
[wsl2]
memory=8GB
swap=2GB
processors=6
nestedVirtualization=true
```
```bash
wsl --shutdown
docker info | grep "CPUs"
```

- AMD on MAC
```bash
docker pull --platform linux/amd64 python:slim
docker run --name sandbox --platform linux/amd64 -w /mnt -v ${PWD}:/mnt -id python:slim
```

### DevOps tools
```bash
#!/bin/bash

apt update -y \
&& apt install -y ansible tmux curl zip unzip jq telnet netcat-traditional net-tools dos2unix git vim nano iputils-ping golang-github-packer-community-winrmcp-dev python3-pip \
&& cd /root \
&& curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl" \
&& chmod +x ./kubectl \
&& mv ./kubectl /usr/local/bin/ \
&& curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 \
&& chmod 700 get_helm.sh \
&& ./get_helm.sh \
&& curl -# -LO https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_Linux_amd64.tar.gz \
&& tar -xzvf eksctl_Linux_amd64.tar.gz \
&& mv eksctl /usr/local/bin/ \
&& curl -# -LO https://releases.hashicorp.com/terraform/1.4.6/terraform_1.4.6_linux_amd64.zip \
&& unzip terraform_1.4.6_linux_amd64.zip \
&& mv terraform /usr/local/bin/ \
&& curl -# -LO https://github.com/gruntwork-io/terragrunt/releases/download/v0.46.3/terragrunt_linux_amd64 \
&& mv terragrunt_linux_amd64 terragrunt \
&& chmod +x terragrunt \
&& mv terragrunt /usr/local/bin/ \
&& curl -LO https://github.com/BurntSushi/ripgrep/releases/download/13.0.0/ripgrep_13.0.0_amd64.deb \
&& dpkg -i ripgrep_13.0.0_amd64.deb \
&& pip3 install boto3 \
&& apt install -y python3-boto3 python3-botocore \
&& curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" \
&& unzip awscliv2.zip \
&& ./aws/install --update \
&& curl -sSL -o /usr/local/bin/argocd https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64 \
&& chmod +x /usr/local/bin/argocd \
&& curl -LO -# https://github.com/derailed/k9s/releases/download/v0.27.4/k9s_Linux_amd64.tar.gz \
&& tar -xzvf k9s_Linux_amd64.tar.gz \
&& chmod +x k9s \
&& cp -rv k9s /usr/local/bin/ \
&& apt-get update -y \
&& apt-get install -y apt-transport-https ca-certificates gnupg curl sudo zip \
&& echo "deb https://packages.cloud.google.com/apt cloud-sdk main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list \
&& curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - \
&& apt-get update -y \
&& apt-get install -y google-cloud-sdk \
&& apt-get install google-cloud-sdk-gke-gcloud-auth-plugin \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/* \
&& rm -rf /tmp/* \
&& rm -rf /var/tmp/* \
&& rm -rf * \
&& curl -o oh-my-zsh-ubuntu.sh https://raw.githubusercontent.com/quickbooks2018/aws/master/oh-my-zsh-ubuntu.sh \
&& chmod +x oh-my-zsh-ubuntu.sh \
&& ./oh-my-zsh-ubuntu.sh \
&& rm -rf *
# End
```

- kubernetes inside single container (Note: below successful testing is done Powerful MAC2)
```bash
#!/bin/bash
# Purpose: Kubernetes Cluster
# extraPortMappings allow the local host to make requests to the Ingress controller over ports 80/443
# node-labels only allow the ingress controller to run on a specific node(s) matching the label selector
# https://kind.sigs.k8s.io/docs/user/ingress/


######################################
# Docker & Docker Compose Installation
######################################
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
rm -f get-docker.sh


#######################
# Kubectl Installation
#######################
curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x ./kubectl
mv ./kubectl /usr/local/bin/kubectl
kubectl version --client

####################
# Helm Installation
####################
# https://helm.sh/docs/intro/install/

curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
cp /usr/local/bin/helm /usr/bin/helm
rm -f get_helm.sh
helm version

###################
# Kind Installation
###################
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-linux-amd64
# curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.11.0/kind-linux-amd64

# Latest Version
# https://github.com/kubernetes-sigs/kind
# curl -Lo ./kind "https://kind.sigs.k8s.io/dl/v0.9.0/kind-$(uname)-amd64"
# curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.9.0/kind-linux-amd64
# curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.8.1/kind-linux-amd64
chmod +x ./kind

mv ./kind /usr/local/bin

# Note: Must add private ip address of machine
#############
# Kind Config
#############
cat << EOF > kind-config.yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
networking:
 apiServerAddress: 0.0.0.0
 apiServerPort: 8443
EOF

  
# kind create --name cloudgeeks cluster --config kind-config.yaml --image kindest/node:v1.21.10
  
  # ssh -N -L 8443:0.0.0.0:8443 cloud_user@d8d0041c.mylabserver.com
  
 # export KUBECONFIG=".kube/config"
  

  
kind create --name cloudgeeks-local cluster --config kind-config.yaml --image kindest/node:v1.25.9
 
export KUBECONFIG=".kube/config"
 
  #End
```

- docker dind for MAC only (Use for Docker builds)
```bash
docker run --name=docker --privileged -id docker:stable-dind
```

- Linux/Windows/MAC CI builds
```bash
docker run --name=podman --privileged --platform=linux/amd64 -w /mnt -id python:slim
docker exec -it podman bash
apt update -y && apt install -y podman curl nano vim
```

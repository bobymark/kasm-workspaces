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
  -e KASM_PORT=443 \
  -p 3000:3000 \
  -p 443:443 \
  -v ${PWD}:/mnt \
  lscr.io/linuxserver/kasm:arm64v8-latest
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
  -e KASM_PORT=8443 \
  -p 3001:3000 \
  -p 8443:8443 \
  -v ${PWD}:/mnt \
  lscr.io/linuxserver/kasm:amd64-latest
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

- Windows
- https://hub.docker.com/r/kasmweb/ubuntu-jammy-desktop
```bash
docker run --name sandbox-kind --shm-size=4096m -v /var/run/docker.sock:/var/run/docker.sock -v "c:/users/Muhammad Asim/Desktop/sandbox:/mnt" -w /mnt -p 6901:6901 -e VNC_PW=password -id kasmweb/ubuntu-jammy-desktop:1.12.0-rolling
```

### DevOps tools
```bash
apt update -y \
&& apt install -y ansible tmux curl zip unzip jq telnet netcat-traditional net-tools dos2unix git vim nano iputils-ping golang-github-packer-community-winrmcp-dev python3-pip \
&& cd /root \
&& curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl" \
&& chmod +x ./kubectl \
&& mv ./kubectl /usr/local/bin/ \
&& curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 \
&& chmod 700 get_helm.sh \
&& ./get_helm.sh \
&& curl -# -LO https://github.com/weaveworks/eksctl/releases/download/v0.94.0-rc.0/eksctl_Linux_amd64.tar.gz \
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
&& rm -rf *
```

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
  -v ${PWD}:/mnt" \
  lscr.io/linuxserver/kasm:arm64v8-latest
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
  -v ${PWD}:/mnt" \
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
## Setup Docker

Docker handles wrapping all projects to reduce dependency chasing.

tl;dr; of [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/) and [Post-install for Linux](https://docs.docker.com/engine/install/linux-postinstall/)

### Add repository and install
```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install -y ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

# Install docker packages
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Add user 1000 to docker group
sudo usermod -aG docker $(id -un 1000)
```

### Add docker-compose convenience script

```bash
sudo tee /usr/local/bin/docker-compose > /dev/null << EOF
#!/bin/bash
docker compose \$(find . -maxdepth 1 -type f \( -name "*.yml" -o -name "*.yaml" \) -exec echo -f {} \; | sort -h) \${@}
EOF
sudo chmod +x /usr/local/bin/docker-compose
```

### Add GCR Image Mirror

This is mostly to avoid hitting Docker Hub pull limits when too lazy to remember to login with an account.  
Also, todo is hosting a pull-through mirror anyway.

```bash
sudo apt-get install -y jq
if [[ ! -e "/etc/docker/daemon.json" ]]; then echo '{}' > /etc/docker/daemon.json ; fi
jq '. |= if has("registry-mirrors") then . else ."registry-mirrors"=["https://mirror.gcr.io"] end' /etc/docker/daemon.json > /tmp/docker-daemon.json && mv /tmp/docker-daemon.json /etc/docker/daemon.json
jq '. |= if ."registry-mirrors" | index("https://mirror.gcr.io") then . else ."registry-mirrors" += ["https://mirror.gcr.io"] end' /etc/docker/daemon.json > /tmp/docker-daemon.json && mv /tmp/docker-daemon.json /etc/docker/daemon.json
systemctl reload docker
```

### Prep common directories
```bash
mkdir -p /srv/{compose,config,data,log}
```

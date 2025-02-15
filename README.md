# PrivaseaAI_Privanetix_Node (Running on VPS2)

**Raised : $15M**

### Update and Upgrade VPS

```
sudo apt update && sudo apt upgrade
sudo apt-get install ca-certificates curl
```

### Install Docker:

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg  
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null  
sudo apt-get update  
sudo apt-get install -y docker-ce docker-ce-cli containerd.io  
docker --version  
```
### Install Docker-Compose:

```
VER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep tag_name | cut -d '"' -f 4)  
sudo curl -L "https://github.com/docker/compose/releases/download/$VER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose  
sudo chmod +x /usr/local/bin/docker-compose  
docker-compose --version  
```

### Docker Permission to User

```
sudo groupadd docker  
sudo usermod -aG docker $USER  
newgrp docker
```

### Pull Privasea docker Image

```
docker pull privasea/acceleration-node-beta:latest
```


### Create the program running directory and navigate to it:

```
mkdir -p  /privasea/config && cd  /privasea
```

### Create a new keystore file 

```
docker run -it -v "/privasea/config:/app/config" privasea/acceleration-node-beta:latest ./node-calc new_keystore
```

Note: The program will prompt you to enter a password, please remember this password for future use. The generated keystore file will have a corresponding node address, please save this address, it will be used in the dashboard configuration


### Change to config directory 

```
cd /privasea/config && ls
```
### Rename the keystore file 

```
mv ./UTC--*  ./wallet_keystore 
```

### Link node address to reward address

- Visit : https://deepsea-beta.privasea.ai/privanetixNode


### Start the node

```
cd /privasea/ 
docker run  -d   -v "/privasea/config:/app/config" -e KEYSTORE_PASSWORD=123456 privasea/acceleration-node-beta:latest
```

**Replace with your password**

### Check Node Health

```
docker logs -f 
```

---

## Update node


### stop node

```
docker ps -q --filter "ancestor=privasea/acceleration-node-beta:latest" | xargs --no-run-if-empty docker stop
docker ps | grep privasea/acceleration-node-beta:latest
```

**Replace with your password**

```
cd /privasea/
docker run  -d   -v "/privasea/config:/app/config" -e KEYSTORE_PASSWORD=123456 privasea/acceleration-node-beta:latest
```


---

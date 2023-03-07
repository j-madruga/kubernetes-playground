El siguiente instructuvo esta realizado utilizando Virtual Box para crear la maquina guest desde Windows 10 como host, utilizando como imagen un Ubuntu 22.04.1 (https://releases.ubuntu.com/jammy/) accediendo via SSH desde Powershell 

### CONFIGURACIÓN PARA ACCEDER POR SSH
- `sudo apt install net-tools` -> nos permite acceder a comandos como **ifconfig**
- apagamos la maquina
- cambiamos la configuración de red a "adaptador puente"
- Volvemos a prender la maquina y hacemos ifconfig, recuperamos la IP de emp0s3 y de ahi a Powershell
- `ssh nombreusuario@ipaddress`

### Docker
- sudo apt-get update
-  sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
- sudo mkdir -m 0755 -p /etc/apt/keyrings
- curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
- echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
-  sudo apt-get update
- sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
- docker --version
- sudo groupadd docker -> crea un grupo
- sudo usermod -aG docker ${USER}
- volver a iniciar sesión -> de esta manera no es necesario poner sudo antes de cada comando de docker, y por lo tanto no falla kind al ejecutar la creación del cluster

### Kind
- curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.17.0/kind-linux-amd64
- chmod +x ./kind
- sudo mv ./kind /usr/local/bin/kind
- export KIND_PATH=/usr/local/Cellar/kind/0.9.0/bin
- export PATH=$PATH:$KIND_PATH
- kind create cluster --name [cluster-name] --config [archivo]

### Kubectl
- curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
- sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
- kubectl version --client

#### CREAR CLUSTER
- kind create cluster --name k8s-playground --config [filename.yaml]

### Zsh (Opcional)
- sudo apt install zsh
- sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
- sudo apt-get install fonts-powerline
- echo "\ue0b0 \u00b1 \ue0a0 \u27a6 \u2718 \u26a1 \u2699" -> para ver si se ven bien los simbolos
- vi ~/.zshrc 
  -> en ZSH-THEME="agnoster"
 -> al final de todo `alias k=kubectl`
- reiniciar la sesión (exit)

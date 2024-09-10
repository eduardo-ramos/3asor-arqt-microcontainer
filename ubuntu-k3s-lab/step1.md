
# Resolução do Trabalho
Antes de mergulharmos na configuração e execução de um cluster Kubernetes em um ambiente Ubuntu Linux, é crucial estabelecer uma base sólida. Este capítulo aborda os pré-requisitos essenciais para garantir que sua máquina virtual (VM) esteja pronta para o processo.

## Pré-requisitos
### Atualizar o sistema operacional
Run `sudo apt-get update`{{exec}}

Com esses pré-requisitos atendidos, sua VM estará pronta para iniciar a configuração do cluster Kubernetes. A seguir, exploraremos os passos detalhados para a criação e gerenciamento do seu cluster.

# Configuração do Kubernetes
## Instalação do Docker
O Kubernetes usa o Docker como mecanismo de contêiner por padrão. Verifique se o Docker está devidamente instalado na máquina virtual que está sendo usada com o seguinte comando:

```bash
docker -v
```{{exec}}

O resultado deverá ser parecido com o exemplo abaixo, do contrário, será necessário instalar o Docker para seguir adiante.

```bash
Docker version 20.10.22, build 3a2c30b
```

Para instalar o Docker, utilize os comandos a seguir:

```bash
sudo apt-get install docker.io -y
sudo systemctl enable docker
sudo systemctl start docker
```{{exec}}

## Instalação do kubeadm, kubelet e kubectl
Kubelet, kubeadm e kubectl são as ferramentas necessárias para criar e gerenciar seu cluster K8S. Através destas ferramentas é possível criar pods, deployments, services, persistent volumes, entre outros recursos utilizados em um cluster.

## Instalação do k3s
Uma alternativa é instalar a ferramenta k3s da CNCF para criar e gerenciar o cluster K8S. O k3s simplifica a criação de clusters K8S, pois traz consigo as ferramentas kubelet, kubeadm e kubectl.
Execute os comandos abaixo no terminal do Ubuntu para instalar o k3s:

### Acessar usuário root
`sudo su`{{exec}}

# Instalar K3S com kubectl
Run `curl -sfL https://get.k3s.io | sh -`{{exec}}

# Habilitar permissão para usuário ubuntu obter configuração de acesso ao K8S
Run `echo K3S_KUBECONFIG_MODE=\"644\" >> /etc/systemd/system/k3s.service.env`{{exec}}

# Restart do serviço k3s para carregar nova config
Run `systemctl restart k3s`{{exec}}

# Logar com usuário ubuntu
Run `su ubuntu`{{exec}}

# Obter informações dos nós do cluster K8S
Run `kubectl get nodes`{{exec}}

# Navega para a pasta do usuário
Run `cd ~`{{exec}}

# Cria o diretório de trabalho para armazenar os arquivos de configuração do cluster
Run `mkdir k8s-cluster`{{exec}}

# Navega para o diretório criado com o comando anterior
Run `cd k8s-cluster`{{exec}}

# Cria o arquivo YAML com as configurações do Persistent Volume Claims
Run `nano wordpress-pvc.yaml`{{exec}}

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: wordpress-pvc
  labels:
    app: wordpress
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: local-path
  resources:
    requests:
      storage: 1Gi
```{{copy}}

## Para fechar e salvar, primeiro digite ctrl + X e quando as opções forem exibidas na parte inferior do editor Nano, digite Y e Enter 

# Cria o arquivo YAML com as configurações do Persistent Volume Claims
Run `nano mysql-pvc.yaml`{{exec}}

```yaml
apiVersion: v1
kind: PersistentVolumeClaim # Permite criarmos volumes persistentes para nossos containers
metadata:
  name: mysql-pvc # Nome da configuração de PVC
  labels:
    app: mysql # Label aplicada no PVC criado, contendo o nome da aplicação
spec:
  accessModes:
    - ReadWriteOnce # Permite que único container acesse o mesmo volume persistente
  storageClassName: local-path
  resources:
    requests:
      storage: 1Gi # Limita o armazenamento em disco do volume em 1GB
```{{copy}}



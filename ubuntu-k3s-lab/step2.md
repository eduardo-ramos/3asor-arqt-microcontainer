## Instalação do kubeadm, kubelet e kubectl
Kubelet, kubeadm e kubectl são as ferramentas necessárias para criar e gerenciar seu cluster K8S. Através destas ferramentas é possível criar pods, deployments, services, persistent volumes, entre outros recursos utilizados em um cluster.

### Instalação do k3s
Uma alternativa é instalar a ferramenta k3s da CNCF para criar e gerenciar o cluster K8S. O k3s simplifica a criação de clusters K8S, pois traz consigo as ferramentas kubelet, kubeadm e kubectl.
Execute os comandos abaixo no terminal do Ubuntu para instalar o k3s:

* Acessar usuário root
```bash
sudo su
```{{exec}}

* Instalar K3S com kubectl
```bash
curl -sfL https://get.k3s.io | sh -
echo K3S_KUBECONFIG_MODE=\"644\" >> /etc/systemd/system/k3s.service.env
```{{exec}}

* Restart do serviço k3s para carregar nova config
```bash
systemctl restart k3s
```{{exec}}

* Em seguida, verifique se o cluster está funcionando, executando o comando abaixo no terminal do Ubuntu para obter as informações dos nós do cluster K8S

```bash
kubectl get nodes
```{{exec}}

### Criação do diretório de trabalho
* Logar com usuário ubuntu
```bash
su ubuntu
```{{exec}}

* Navegar para a pasta do usuário ubuntu
```bash
cd ~
```{{exec}}

* Depois, crie o diretório de trabalho para armazenar os arquivos de configuração do cluster e navegue para o diretório criado com o comando anterior.
```bash
mkdir k8s-cluster
cd k8s-cluster
```{{exec}}

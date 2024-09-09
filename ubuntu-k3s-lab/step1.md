
# Atualizar o sistema operacional
Run `sudo apt-get update && sudo apt-get upgrade -y`{{exec}}

# Acessar usuário root
Run `sudo su`{{exec}}

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

```
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

# Cria o arquivo YAML com as configurações do Persistent Volume Claims
Run `nano mysql-pvc.yaml`

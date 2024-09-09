
# Atualizar o sistema operacional
Run `sudo apt-get update && sudo apt-get upgrade -y`

# Acessar usuário root
Run `sudo su`

# Instalar K3S com kubectl
Run `curl -sfL https://get.k3s.io | sh -`

# Habilitar permissão para usuário ubuntu obter configuração de acesso ao K8S
Run `echo K3S_KUBECONFIG_MODE=\"644\" >> /etc/systemd/system/k3s.service.env`

# Restart do serviço k3s para carregar nova config
Run `systemctl restart k3s`

# Logar com usuário ubuntu
Run `su ubuntu`

# Obter informações dos nós do cluster K8S
Run `kubectl get nodes`

# Navega para a pasta do usuário
Run `cd ~`

# Cria o diretório de trabalho para armazenar os arquivos de configuração do cluster
Run `mkdir k8s-cluster`

# Navega para o diretório criado com o comando anterior
Run `cd k8s-cluster`

# Cria o arquivo YAML com as configurações do Persistent Volume Claims
Run `nano wordpress-pvc.yaml`

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

```

# Cria o arquivo YAML com as configurações do Persistent Volume Claims
Run `nano mysql-pvc.yaml`

## Aplicação das configurações
TBD
```bash
# Aplicar a configuração de PVC (wordpress-pvc)
kubectl apply -f wordpress-pvc.yaml

# Aplicar a configuração de PVC (mysql-pvc)
kubectl apply -f mysql-pvc.yaml

# Aplicar a configuração de Deployment (wordpress-deployment)
kubectl apply -f wordpress-deployment.yaml

# Aplicar a configuração de Deployment (mysql-deployment)
kubectl apply -f mysql-deployment.yaml

# Aplicar a configuração de Service (wordpress-service)
kubectl apply -f wordpress-service.yaml

# Aplicar a configuração de Service (mysql-service)
kubectl apply -f mysql-service.yaml

# Aplicar a configuração de Ingress (wordpress-ingress)
kubectl apply -f wordpress-ingress.yaml
```{{exec}}

Para exibir todos os pods criados no cluster K8S, utilizar novamente o comando:
```bash
kubectl get pods
```{{exec}}

O resultado desse comando deve exibir a lista dos pods criados.
```bash
ubuntu@ubuntu:~/k8s-cluster$ kubectl get pods
NAME                                    READY   STATUS              RESTARTS   AGE
mysql-deployment-6fb4446c74-4bfsg       0/1     ContainerCreating   0          21s
wordpress-deployment-6d4c5d9689-hj8s5   0/1     ContainerCreating   0          22s
wordpress-deployment-6d4c5d9689-md8cf   0/1     ContainerCreating   0          22s
wordpress-deployment-6d4c5d9689-ntpfx   0/1     ContainerCreating   0          22s
```

Obs: O status _ContainerCreating_ indica que os containers Docker ainda estão sendo criados pelo cluster. Continue executando o comando `kubectl get pods` até que o status de todos mude para _Running_.
```bash
# Apenas um dos pods está com status Running
ubuntu@ubuntu:~/k8s-cluster$ kubectl get pods
NAME                                    READY   STATUS              RESTARTS   AGE
mysql-deployment-6fb4446c74-4bfsg       1/1     Running             0          46s
wordpress-deployment-6d4c5d9689-hj8s5   0/1     ContainerCreating   0          47s
wordpress-deployment-6d4c5d9689-md8cf   0/1     ContainerCreating   0          47s
wordpress-deployment-6d4c5d9689-ntpfx   0/1     ContainerCreating   0          47s

# Agora todos os pods estão ativos e podem ser testados sem riscos de quebra
ubuntu@ubuntu:~/k8s-cluster$ kubectl get pods
NAME                                    READY   STATUS    RESTARTS   AGE
mysql-deployment-6fb4446c74-4bfsg       1/1     Running   0          61s
wordpress-deployment-6d4c5d9689-hj8s5   1/1     Running   0          62s
wordpress-deployment-6d4c5d9689-md8cf   1/1     Running   0          62s
wordpress-deployment-6d4c5d9689-ntpfx   1/1     Running   0          62s
```

# Configuração dos recursos Kubernetes
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

Para aplicar todos os arquivos .yaml da pasta corrente, utilizar o seguinte comando:
```bash
kubectl apply -f .
```{{exec}}

  
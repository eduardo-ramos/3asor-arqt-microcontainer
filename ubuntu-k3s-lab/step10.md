# Testes de Resiliência
TBD.

### Simulação da perda de todos os pods simultâneamente
Liste todos os pods em execução no cluster, sem aplicar nenhum filtro dessa.

```bash
kubectl get pods
```{{exec}}

Em seguida, apagamos todos os pods em execução com o comando abaixo:

```bash
# Certifique-se que está na pasta de trabalho do k3s
cd ~/k8s-cluster

#Este comando exclui todos os pods com base nos arquivos de configuração
kubectl delete -f .
```{{exec}}

### Verificação da integridade dos dados
Para verificar a integridade dos pods removidos, acesse novamente ou atualize o site WordPress para verificar o comportamento.

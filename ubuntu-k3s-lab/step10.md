# Testes de Resiliência
### Simulação da perda de todos os pods simultâneamente
Liste todos os pods em execução no cluster, sem aplicar nenhum filtro dessa.

```bash
kubectl get pods
```{{exec}}

Em seguida, apagamos todos os pods em execução com o comando abaixo:

```bash
kubectl delete pods $(kubectl get pods -o json | jq -r '.items[] | select(.metadata.name).metadata.name')
```{{exec}}

### Verificação da integridade dos dados
Para verificar a integridade dos pods removidos, acesse novamente ou atualize o site WordPress para verificar o comportamento.

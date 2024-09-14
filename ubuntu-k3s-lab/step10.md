# Testes de Resiliência
### Simulação da perda de todos os pods simultâneamente
Finalmente, a simulação da perda de todos os pods simultâneamente tem por objetivo garantir que o Wordpress e o MySQL continuem funcionando normalmente após a perda de todos os seus pods.
Neste teste, apagamos todos os pods em execução do cluster. Mesmo que os pods sejam deletados, estes devem se restabelecer automaticamente, de forma que o Wordpress e o MySQL continuem funcionando normalmente.

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

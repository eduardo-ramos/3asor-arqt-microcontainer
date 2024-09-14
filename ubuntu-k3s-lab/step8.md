# Testes de Resiliência
## Simulação da perda dos pods do WordPress
Primeiramente, listamos todos os pods em execução no cluster, filtrando pelos pods do WordPress.

```bash
kubectl get pods | grep wordpress
```{{exec}}

Em seguida, apagamos os pods do WordPress com o comando abaixo:

```bash
kubectl delete pods $(kubectl get pods -o json | jq -r '.items[] | select(.metadata.name | test("wordpress-")).metadata.name')
```{{exec}}

### Verificação da integridade dos dados do WordPress
Para verificar a integridade dos pods removidos, acesse novamente ou atualize o site WordPress para verificar o comportamento.

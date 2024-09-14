
kubectl delete pods $(kubectl get pods -o json | jq -r '.items[] | select(.metadata.name | test("wordpress-")).metadata.na
me')

## Fique atento
### Antes de executar algum comando, certifique-se que o comando anterior foi concluído com sucesso.

### Antes de salvar os arquivos no editor Nano, certifique-se que o foco do cursor está ativo no editor
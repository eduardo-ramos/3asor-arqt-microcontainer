
kubectl delete pods $(kubectl get pods -o json | jq -r '.items[] | select(.metadata.name | test("wordpress-")).metadata.na
me')
-----note: don't use this way to deploy, use helm. this is just for demonstration on how to deploy using kubectl commands-----

1. kubectl create -f vault.yaml

2. kubectl port-forward svc/vault-elb-int 7000:8200

3. curl http://localhost:7000/v1/sys/health

4. http://127.0.0.1:7000/ui/vault/auth?with=token

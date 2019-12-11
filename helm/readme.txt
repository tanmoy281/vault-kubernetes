to deploy: helm install vault vault-k8s

to delete: helm delete vault

to upgrade image : kubectl edit deployment <deployment_name> , now change the image and save. Pod will automatically be created
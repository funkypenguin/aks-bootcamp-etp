# aks-bootcamp-etp

## Create cluster
```
az group create --name rg-aks-bootcamp --location australiaeast

az ad sp create-for-rbac \
    --name http://sp-aksbootcamp \
    --skip-assignment

SP_ID=<replace with service principal ID>
SP_PASS=<replace with service principal key>

az group deployment create \
    --resource-group rg-aks-bootcamp \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-aks/azuredeploy.json \
    --parameters    "clusterName=aksbootcamp" \
                    "location=australiaeast" \
                    "dnsPrefix=aksbootcamp" \
                    "linuxAdminUsername=azureuser" \
                    "sshRSAPublicKey=ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCgdQOZR7Xhf/Jwpx2egp19kPkESyh8LFcZDAYmee34QGrdI3Fjo72CjC1vbt2V8tSpS+9fZjW8jTszh+t6xMxc+psJtMtv15EgVDl7vZmT1AwLyqqy5ggoujddnAuf0CvOPNNsvVH43xoYpU/j2NqTb6kGEKdGf8FRVxUyXWCwQXTZIFLJnNM7DtXSVzQ8KkYPHthxVl6GZgY7MgVN7NKv4CYqzOQaVXCo9rcl6+3y4NOM+2WC4IMgblhDeUY75tf7gkEv+MXDk9MuSuvldMAYN6sL0pHS0V7BlYjA8td8+PhG9qKrZMZSxDx7oUYaTZoW0qNOTwtWtzUsBjf6Ph+J funkypenguin@david-macbook.funkypenguin.co.nz" \
                    "servicePrincipalClientId=$SP_ID" \
                    "servicePrincipalClientSecret=$SP_PASS" \
                    "kubernetesVersion=1.13.5"
```
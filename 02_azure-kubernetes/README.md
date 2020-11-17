# Setup a Kubernetes Cluster

Use the below CLI commands to provision Azure Kubernetes Service (AKS) cluster.

> NOTE: This requires the `$NAME` and `$LOCATION` variables set from the [prerequisites](/00_prequisites/README.md).

## Create Kubernetes Cluster

```bash
# Create cluster
az aks create \
--resource-group $NAME \
--name $NAME \
--location $LOCATION \
--kubernetes-version 1.18.10 \
--generate-ssh-keys \
--enable-managed-identity

# --enable-addons monitoring

# Delete cluster
az aks delete \
--resource-group $NAME \
--name $NAME
```

# Setup Azure Arc

We will use Azure Arc to inturn setup FluxCD to apply cluster resources to Kubernets.

## Azure CLI Prerequisites

As part of this demo, make sure all of the preview extensions are up to date.

```bash
az extension add --name connectedk8s
az extension add --name k8sconfiguration

az extension update --name aks-preview
az extension update --name connectedk8s
az extension update --name k8sconfiguration
```

## Add Cluster to Azure Arc

> NOTE: This requires the `$NAME` and `$LOCATION` variables set from the [prerequisites](/00_prequisites/README.md).

```bash
# Make sure you have logged into the cluster before executing the final step.
az aks get-credentials -g $NAME -n $NAME

# Setup the connectiont to Azure Arc
az connectedk8s connect --resource-group $NAME --name $NAME --location $LOCATION

# az k8sconfiguration create \
# --name apim-demo \
# --cluster-name $NAME \
# --resource-group $NAME \
# --operator-instance-name apim-demo \
# --operator-namespace cluster-config \
# --repository-url https://github.com/Azure/arc-k8s-demo \
# --scope cluster \
# --cluster-type connectedClusters
```

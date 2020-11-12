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
```

## Add FluxCD to Arc-enabled Cluster

Azure Arc enables quick and easy configuration of FluxCD on your cluster.

![Azure Arch Configuration](/assets/arc-screenshot-1.png)

```bash
# TODO: Here's how you can do it with the CLI
# az k8sconfiguration create \
# --name apim-demo \
# --cluster-name $NAME \
# --resource-group $NAME \
# --operator-instance-name apim-demo \
# --operator-namespace cluster-config \
# --repository-url https://github.com/Azure/arc-k8s-demo \
# --scope cluster \
# --cluster-type connectedClusters \
# --git-branch main \
# --git-path flux
```

## Verify Setup

Make sure the API that has been deployed is accessible from within the cluster. Busybox is a simple way to test from within a cluster.

```bash
kubectl run curl-cdw --image=radial/busyboxplus:curl -i --tty --rm

curl http://svcdiscsvc.svcdisc-demo/data
```

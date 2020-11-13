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
az connectedk8s connect --resource-group $NAME --name $NAME --location $LOCATION
```

## Add FluxCD to Arc-enabled Cluster

Azure Arc enables quick and easy configuration of FluxCD on your cluster.

![Azure Arch Configuration](/assets/arc-screenshot-1.png)

```bash
# TODO: Here's how you can do it with the CLI
# az k8sconfiguration create \
# --name flux \
# --cluster-name $NAME \
# --resource-group $NAME \
# --operator-instance-name flux \
# --operator-namespace flux \
# --repository-url https://github.com/cwiederspan/apim-fulldemo-20201111.git \
# --scope cluster \
# --cluster-type connectedClusters \
# --enable-helm-operator true \
# --git-branch main \
# --git-path flux \
# --git-readonly
```

## Verify Setup

Make sure the API that has been deployed is accessible from within the cluster. Busybox is a simple way to test from within a cluster.

```bash
kubectl run curl-cdw --image=radial/busyboxplus:curl -i --tty --rm

curl http://svcdiscsvc.svcdisc-demo/data
```

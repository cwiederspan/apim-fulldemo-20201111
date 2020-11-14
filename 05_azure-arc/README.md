# Setup Azure Arc

We will use Azure Arc to in turn setup FluxCD to apply cluster resources to Kubernets.

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
az k8sconfiguration create \
--name flux \
--cluster-name $NAME \
--resource-group $NAME \
--scope cluster \
--cluster-type connectedClusters \
--operator-namespace flux \
--operator-instance-name flux \
--repository-url https://github.com/cwiederspan/apim-fulldemo-20201111.git \
--git-branch main \
--git-path flux \
--git-readonly
--enable-helm-operator \
--helm-operator-version='1.2.0' \
--helm-operator-params='--set helm.versions=v3'

# Demo from https://docs.microsoft.com/en-us/azure/azure-arc/kubernetes/use-gitops-with-helm
az k8sconfiguration create \
--name azure-arc-sample \
--cluster-name $NAME \
--resource-group $NAME \
--scope namespace \
--cluster-type connectedClusters \
--repository-url https://github.com/Azure/arc-helm-demo.git \
--operator-instance-name fluxhelm \
--operator-namespace arc-k8s-demo \
--operator-params='--git-readonly --git-path=releases' \
--enable-helm-operator \
--helm-operator-version='1.2.0' \
--helm-operator-params='--set helm.versions=v3'

az k8sconfiguration delete \
--name azure-arc-sample \
--cluster-name $NAME \
--cluster-type connectedClusters \
--resource-group $NAME

```

## Verify Setup

Make sure the API that has been deployed is accessible from within the cluster. Busybox is a simple way to test from within a cluster.

```bash
kubectl run curl-cdw --image=radial/busyboxplus:curl -i --tty --rm

curl http://svcdiscsvc.svcdisc-demo/data
```

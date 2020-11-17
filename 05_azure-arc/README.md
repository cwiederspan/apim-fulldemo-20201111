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
# Create the Flux config with the CLI
az k8sconfiguration create \
--name flux-cluster-01 \
--cluster-name $NAME \
--resource-group $NAME \
--scope cluster \
--cluster-type connectedClusters \
--operator-namespace flux-cluster-01 \
--operator-instance-name flux \
--operator-params '--git-readonly --git-branch main --git-path flux --manifest-generation=true --git-poll-interval=3m' \
--repository-url https://github.com/cwiederspan/apim-fulldemo-20201111.git \
--enable-helm-operator \
--helm-operator-version='1.2.0' \
--helm-operator-params='--set helm.versions=v3'

# Delete the Flux config with the CLI
az k8sconfiguration delete \
--name my-flux \
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

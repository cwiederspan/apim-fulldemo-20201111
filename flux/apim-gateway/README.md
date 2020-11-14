# API Gateway via Flux

## Connect to the AKS Cluster

> NOTE: This requires the `$NAME` and `$LOCATION` variables set from the [prerequisites](/00_prequisites/README.md).

```bash
az aks get-credentials -g $NAME -n $NAME
```

## Secrets for APIM Gateway

When you create the self-hosted gateway for the API Management service, you
will be provided with instructions for deployment. You will need to translate
these steps into a config.yaml file, which will then need to be applied to the
cluster manually.

> NOTE: Use the [config-sample.yaml](config-sample.yaml) file as a template.

## Apply the Config

Now that we have a full set of config and secrets, apply the config.yaml file.

```bash
kubectl apply -f config.yaml
```

## Add a Flux Config for API Gateway

> NOTE: The `operator-namespace` must match the value provided in [kustomization.yaml](kustomization.yaml).

```bash
# Create
az k8sconfiguration create \
--name apim-gateway \
--cluster-name $NAME \
--resource-group $NAME \
--cluster-type connectedClusters \
--scope namespace \
--operator-namespace apim-gateway \
--operator-instance-name apim-gateway \
--repository-url https://github.com/cwiederspan/apim-fulldemo-20201111.git \
--git-branch main \
--git-path 'flux/apim-gateway' \
--git-readonly

# Delete
az k8sconfiguration delete \
--name azure-arc-sample \
--cluster-name $NAME \
--cluster-type connectedClusters \
--resource-group $NAME
```

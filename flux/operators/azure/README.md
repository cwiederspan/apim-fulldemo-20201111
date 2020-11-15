# Azure Service Operator via Flux

## Setup Helm Secrets for Azure Operator

Create a Service Principal that will be used by the Azure Operator to communicate back to
Azure when it needs to create resources in the subscription. After creating the SP using
the script below, copy the resulting values into the same config.yaml file as above.

```bash
# Create a Service Principal
az ad sp create-for-rbac \
-n <<YOUR_SP_NAME>> \
--role contributor \
--scopes /subscriptions/<<YOUR_SUBSCRIPTION_ID>>
```

> NOTE: Use the [config-sample.yaml](config-sample.yaml) file as a template.

## Apply the Config

Now that we have a full set of config and secrets, apply the config.yaml file.

```bash
kubectl apply -f config.yaml
```

## Add a Flux Config for API Gateway

> NOTE: The `operator-namespace` must match the value provided in [kustomization.yaml](kustomization.yaml).

> NOTE: This must be a **cluster** scoped install.

```bash
# Create
az k8sconfiguration create \
--name azure-operator \
--resource-group $NAME \
--cluster-name $NAME \
--cluster-type connectedClusters \
--scope cluster \
--operator-namespace azure-operator \
--operator-instance-name flux \
--repository-url https://github.com/cwiederspan/apim-fulldemo-20201111.git \
--operator-params '--git-readonly --git-branch main --git-path flux/operators/azure --manifest-generation=true --git-poll-interval=3m' \
--enable-helm-operator \
--helm-operator-version='1.2.0' \
--helm-operator-params='--set helm.versions=v3'

# Delete
az k8sconfiguration delete \
--name azure-operator \
--resource-group $NAME \
--cluster-name $NAME \
--cluster-type connectedClusters
```

# Setup Config and Secrets

## Connect to the AKS Cluster

> NOTE: This requires the `$NAME` and `$LOCATION` variables set from the [prerequisites](/00_prequisites/README.md).

```bash
az aks get-credentials -g $NAME -n $NAME
```

# Setup Helm Secrets for Azure Operator

Create a Service Principal that will be used by the Azure Operator to communicate back to
Azure when it needs to create resources in the subscription. After creating the SP using the script below, copy the resulting values into the same config.yaml file as above.

```bash
# Create a Service Principal
az ad sp create-for-rbac \
-n <<YOUR_SP_NAME>> \
--role contributor \
--scopes /subscriptions/<<YOUR_SUBSCRIPTION_ID>>
```

## Apply the Config

Now that we have a full set of config and secrets, apply the config.yaml file.

```bash
kubectl apply -f config.yaml
```

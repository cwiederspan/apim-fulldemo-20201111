# Setup Config and Secrets

## Secrets for APIM Gateway

When you create the self-hosted gateway for the API Management service, you
will be provided with instructions for deployment that will look like the
steps below.

```bash
# Create the secret - you get this value from the Azure Portal
# when you setup the self-hosted gateway.
kubectl create secret generic kubernetes-token \
--from-literal=value="GatewayKey xxxyyyzzz==" \
--type=Opaque
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
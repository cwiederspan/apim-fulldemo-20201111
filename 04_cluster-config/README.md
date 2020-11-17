# Setup Config and Secrets

Before proceeding, we will need to setup some secrets and configuration values in the cluster
so that other tools like Flux and APIM will have what they need to spin up once we begin
deploying them through Flux. Because we do not want to include these secrets in our git repo,
we must do this _out of band_.

> NOTE: Use the [config-sample.yaml](config-sample.yaml) file as a template for the `config.yaml`
> file mentioned in the steps below.

## Secrets for APIM Gateway

When you create the self-hosted gateway for the API Management service, you
will be provided with instructions for deployment. You will need to translate
these steps into a `config.yaml` file, which will then need to be applied to the
cluster manually.

## Secrets for Azure Operator

Create a Service Principal that will be used by the Azure Operator to communicate back to
Azure when it needs to create resources in the subscription. After creating the SP using
the script below, copy the resulting values into the same `config.yaml` file as above.

```bash
# Create a Service Principal
az ad sp create-for-rbac \
-n <<YOUR_SP_NAME>> \
--role contributor \
--scopes /subscriptions/<<YOUR_SUBSCRIPTION_ID>>
```

## Apply the Config

Now that we have a full set of config and secrets, apply the `config.yaml` file.

```bash
kubectl apply -f config.yaml
```

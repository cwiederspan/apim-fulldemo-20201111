# Setup Secrets for APIM Gateway

When you create the self-hosted gateway for the API Management service, you
will be provided with instructions for deployment that will look like the
steps below.

```bash

# Create the secret - you get this value from the Azure Portal
# when you setup the self-hosted gateway.
kubectl create secret generic kubernetes-token \
--from-literal=value="GatewayKey xxxyyyzzz==" \
--type=Opaque

# Copy/Create the config.yaml file and execute
kubectl apply -f config.yaml

```

# Setup API Management

Use the below CLI commands to provision APIM.

> NOTE: This requires the `$NAME` and `$LOCATION` variables set from the [prerequisites](/00_prequisites/README.md).

```bash

az apim create \
  --resource-group $NAME \
  --name $NAME \
  --location $LOCATION \
  --publisher-email chwieder@microsoft.com \
  --publisher-name CDWMS \
  --sku-name Developer \
  --virtual-network External

  # [--enable-client-certificate {false, true}]
  # [--enable-managed-identity {false, true}]
```


# Setup APIM Product and API

```bash

az apim product create \
--product-name Private \
--resource-group $NAME \
--service-name $NAME \
--description 'Group of APIs that allow access to on-prem APIs hosted in Kubernetes' \
--state published

# [--approval-required]
# [--legal-terms]
# [--no-wait]
# [--product-id]
# [--subscription]
# [--subscription-required]
# [--subscriptions-limit]

az apim api create \
--api-id service-discovery \
--resource-group $NAME \
--service-name $NAME \
--display-name 'Service Discovery' \
--description 'A backend service discovery tester' \
--service-url 'http://svcdiscsvc.svcdisc-demo' \
--path svcdisc

# [--api-type {http, soap}]
# [--authorization-scope]
# [--authorization-server-id]
# [--bearer-token-sending-methods]
# [--no-wait]
# [--open-id-provider-id]
# [--protocols {http, https}]
# [--subscription]
# [--subscription-key-header-name]
# [--subscription-key-query-param-name]
# [--subscription-key-required]
# [--subscription-required {false, true}]

```

# Demo Execution

## Add Cluster to Azure Arc

Make sure you have logged into the cluster before executing the final step.

```bash

az aks get-credentials -g $NAME -n $NAME

az connectedk8s connect --resource-group $NAME --name $NAME --location $LOCATION

```

## Setup the Secrets for the Gateway

[See /config README](/config/README.md)

## Deploy the Gateway

```bash

cd flux/apim-gateway

kubectl apply -f gateway.yaml

```

*TODO:* Make sure the APIs are setup and attached to the new gateway.

## Deploy the First Sample App

```bash

cd flux/akssvcdisc

kubectl apply -f deployment.yaml

# Test the new API
kubectl run curl-cdw --image=radial/busyboxplus:curl -i --tty --rm

curl http://svcdiscsvc1/data

```

## Setup a Product for the Private APIs

## Setup an API for the New API



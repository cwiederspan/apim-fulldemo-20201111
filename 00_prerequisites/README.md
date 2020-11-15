# Setup Various Prerequisites

## Azure CLI Prerequisites

As part of this demo, make sure all of the preview extensions are up to date.

```bash
az extension add --name connectedk8s
az extension add --name k8sconfiguration

az extension update --name aks-preview
az extension update --name connectedk8s
az extension update --name k8sconfiguration
```

## Setup Shell Variables

These variables will be used throughout the demo.

```bash
NAME=cdw-apimgmt-20201113

# Azure Arc is limited to East US (among a few others), so use it
LOCATION=eastus
```

## Create an Azure Resource Group

```bash
az group create -n $NAME -l $LOCATION
```

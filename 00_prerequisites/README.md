# Setup Various Prerequisites

## Setup Shell Variables

These variables will be used throughout the demo.

```bash
NAME=cdw-apimgmt-20201112

# Azure Arc is limited to East US (among a few others), so use it
LOCATION=eastus
```

## Create an Azure Resource Group

```bash
az group create -n $NAME -l $LOCATION
```

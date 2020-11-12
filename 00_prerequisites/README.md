# Setup Various Prerequisites

## Setup Shell Variables

These variables will be used throughout the demo.

```bash
NAME=cdw-apimgmtdemo-20201111

# Azure Arc is limited to East US (among a few others), so use it
LOCATION=eastus
```

## Create an Azure Resource Group

```bash
az group create -n $NAME -l $LOCATION
```
